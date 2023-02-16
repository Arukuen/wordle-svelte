<script lang='ts'>
  export let title:string;
</script>


<div class="header">
  <p>
    {#each title as letter}
      <span>{letter}</span>
    {/each}
  </p>
</div>


<style>
  .header {
    color: #ddd;
    border-bottom: 1px solid grey;
    padding: 15px;
  }

  p {
    text-align: center;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    font-weight: bold;
    font-size: xxx-large;
    margin: 0;
  }

  span:nth-child(4n + 1) {
    color: #4285F4;
  }

  span:nth-child(4n + 2) {
    color: #DB4437;
  }

  span:nth-child(4n + 3) {
    color: #F4B400;
  }

  span:nth-child(4n + 4) {
    color: #0F9D58;
  }
</style>