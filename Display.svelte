<script lang="ts">
    export let rows: number;
    export let cols: number;
    export let currentRow: number;
    export let currentWord: string;

    let list: string[][] = [];
    for (let i = 0; i < rows; i++) {
      let temp = []
      for (let j = 0; j < cols; j++) {
        temp.push('');
      }
      list.push(temp);
    }

    $: list[currentRow] = [...currentWord, ...new Array(5 - currentWord.length).fill('')];
</script>


<div class="display">
  <table>
    {#each list as row}
      <tr>
        {#each row as letter}
          {#if letter == ''}
            <td>&nbsp;</td>
          {:else}
            <td>{letter}</td>
          {/if}
        {/each}
      </tr>
    {/each}
  </table>
</div>


<style>
  .display {
    color: white;
    font-size: 35px;
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  }

  table {
    margin: 20px;
    margin-left: auto;
    margin-right: auto;
    border-spacing: 5px;
  }

  td {
    border: 3px solid black;
    width: 45px;
    height: 45px;
    background-color: black;
    border: 1px solid grey;
    padding: 5px;
  }

  .correct {
    background-color: #528d4f;
  }

  .misplaced {
    background-color: #b49f3a;
  }

  .incorrect {
    background-color: darkgray;
  }
</style>