<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  const letters = ['Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '/', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', '/', 'Delete', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', 'Enter'];
  
  const handleKeyboard = (letter) => {
    dispatch('keyboard', {letter: letter});
  }
</script>


<div class="keyboard">
  {#each letters as letter}
    {#if letter !== '/'}
      <button class:special="{letter === 'Delete' || letter === 'Enter'}" on:click={() => handleKeyboard(letter)}>{letter}</button>
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
    width: 100px;
  }
</style>