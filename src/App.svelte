<script lang="ts">
	import Keyboard from "./Keyboard.svelte";
	import Display from "../Display.svelte";
	import Header from "./Header.svelte";

	const url = 'https://gist.githubusercontent.com/shmookey/b28e342e1b1756c4700f42f17102c2ff/raw/ed4c33a168027aa1e448c579c8383fe20a3a6225/WORDS';
	let wordInput = '';
	let randomWord = '';
	let handleEnter;
	let isDone = false;


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
				handleEnter();
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


<Header title="Woooooooordle"/>
<main>
	{#await main()}
		<p>Loading...</p>
	{:then value} 
		<Display rows={6} cols={5} currentWord={wordInput} randomWord={randomWord} bind:handleEnter={handleEnter} bind:isDone={isDone}/>
		<Keyboard on:keyboard={handleKeyInput} disabled={isDone}/>
	{/await}
</main>


<style>
	main {
		text-align: center;
		max-width: 720px;
		margin: 0 auto;
	}
</style>