<script lang="ts">
    export let rows: number;
    export let cols: number;

    import { each } from "svelte/internal";
    let list: string[][] = [];
    for (let i = 0; i < rows; i++) {
      let temp = []
      for (let j = 0; j < cols; j++) {
        temp.push('A');
      }
      list.push(temp);
    }
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
    font-size: xx-large;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: bold;
  }

  table {
    margin: 20px;
    margin-left: auto;
    margin-right: auto;
  }

  td {
    border: 3px solid black;
    width: 50px;
    height: 55px;
    background-color: goldenrod;
  }
</style>