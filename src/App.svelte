<script lang="ts">
	import Keyboard from "./Keyboard.svelte";
	import Display from "../Display.svelte";
	import Header from "./Header.svelte";

	const url = 'https://gist.githubusercontent.com/dracos/dd0668f281e685bad51479e5acaadb93/raw/ca9018b32e963292473841fb55fd5a62176769b5/valid-wordle-words.txt';
	let wordInput = '';
	let randomWord = '';
	let dispComp;

	const fetchRandomWord = async () => {
		let response = await fetch(url);
	
		if (response.status === 200) {
				let strList = await response.text();
				let wordList = strList.split('\n');
				let randomIndex = Math.floor(Math.random() * wordList.length)
				let word = wordList[randomIndex];
        return word;
    }
	}

	const handleKeyInput = (e:any) => {
		let letter:string = e.detail.letter;
		
		if (letter === 'Backspace') {
			if(wordInput.length > 0) {
				wordInput = wordInput.slice(0, -1);
			}
		}
		else if (letter === 'Enter'){
			if(wordInput.length === 5){
				wordInput = '';
				dispComp.handleEnter();
			}
		}
		else {
			if (wordInput.length < 5)
				wordInput += letter.toUpperCase();
		}
	}

	const main = async() => {
		randomWord = await fetchRandomWord();
		randomWord = randomWord.toUpperCase()
		console.log(randomWord);
	}
</script>


<Header title="Georgina's Wordle"/>
<main>
	{#await main()}
		<p>Loading...</p>
	{:then value} 
		<Display rows={6} cols={5} currentWord={wordInput} randomWord={randomWord} bind:this={dispComp}/>
		<Keyboard on:keyboard={handleKeyInput}/>
	{/await}
</main>


<style>
	main {
		text-align: center;
		max-width: 720px;
		margin: 0 auto;
	}
</style>