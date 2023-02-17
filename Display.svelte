<script lang="ts">
    export let rows: number;
    export let cols: number;
    export let currentWord: string;
    export let randomWord: string;
    export let isDone = false;
    export let isWinner = false;

    let currentRow = 0;
    let toggleCheck = new Array(cols - currentWord.length).fill(false);
    let wordPerRow = [];
    

    export const handleEnter = () => {
      $: toggleCheck[currentRow] = true;
      wordPerRow.push(currentWord);
      currentRow++;

      if (currentWord == randomWord){
        isDone = true;
        isWinner = true;
      }
      if (currentRow >= rows) {
        isDone = true;
      }
    }

    const compareLetter = (row_index, col_index) => {
      if (wordPerRow[row_index][col_index] === randomWord[col_index])
        return 'correct';
      else if (randomWord.includes(wordPerRow[row_index][col_index]))
        return 'misplaced';
      else
        return 'incorrect';
    }
  

    let list: string[][] = [];
    for (let i = 0; i < rows; i++) {
      let temp = []
      for (let j = 0; j < cols; j++) {
        temp.push('');
      }
      list.push(temp);
    }

    $:{
    if (!isDone)
      list[currentRow] = [...currentWord, ...new Array(cols - currentWord.length).fill('')];
    }
</script>


<div class="display">
  <table>
    {#each list as row, row_index}
      <tr>
        {#each row as letter, col_index}
          {#if letter == ''}
            <td>&nbsp;</td>
          {:else}
            {#if toggleCheck[row_index]}
              <td class="{compareLetter(row_index, col_index)}">{letter}</td>
            {:else}
              <td>{letter}</td>
            {/if}
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