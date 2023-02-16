<script>
  import { createEventDispatcher } from 'svelte';

  export let disabled = false;

  const dispatch = createEventDispatcher();
  const letters = ['Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '/', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', '/',
   'Backspace', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', 'Enter'];
  
  const handleKeyboard = (letter) => {
    if (disabled)
      return;
    dispatch('keyboard', {letter: letter});
  }

  const handleKeydown = (e) => {
    if (disabled)
      return;
    if ((e.keyCode >= 65 && e.keyCode <= 90) || (e.keyCode === 8) || e.keyCode === 13)
      dispatch('keyboard', {letter: e.key})
  }
</script>

<svelte:window on:keydown={handleKeydown}/>

<div class="keyboard">
  {#each letters as letter}
    {#if letter !== '/'}
      <button class:special="{letter === 'Backspace' || letter === 'Enter'}" on:click={() => handleKeyboard(letter)}>{letter}</button>
    {:else}
      <br />
    {/if}
    
  {/each}
</div>

<style>
  button {
    width: 55px;
    height: 60px;
    margin: 0;
    padding: 10px 20px;
    color: white;
    background-color: grey;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: bold;
    border: 3px solid black;
    border-radius: 10px;
  }

  .special {
    width: 130px;
  }
</style>