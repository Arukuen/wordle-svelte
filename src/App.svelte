<script lang="ts">
	import Keyboard from "./Keyboard.svelte";
	import Display from "../Display.svelte";
	import Header from "./Header.svelte";

	const url = 'https://gist.githubusercontent.com/dracos/dd0668f281e685bad51479e5acaadb93/raw/ca9018b32e963292473841fb55fd5a62176769b5/valid-wordle-words.txt';

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
		console.log(e.detail.letter)
	}

	let x:string = 'Loading...';

	const main = async() => {
		x = await fetchRandomWord();
	}

	
	main();
</script>

<Header title="Wordle"/>
<main>
	<Display rows={6} cols={5}/>
	<Keyboard on:keyboard={handleKeyInput}/>
	<p>{x}</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 720px;
		margin: 0 auto;
	}

	p {
		color: white;
	}
</style>