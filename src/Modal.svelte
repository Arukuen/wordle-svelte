<script lang="ts">
  export let message;
  export let showModal;
  export let isWinner;
</script>

{#if showModal}
<div class='backdrop' on:mousedown>
  <div class="modal" class:winner={isWinner}>
    <p>{message}</p>
  </div>
</div>
{/if}


<style>
  .backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.7);
  }

  .modal {
    margin: 10% auto;
    max-width: 400px;
    padding: 10px;
    border-radius: 10px;
    color: white;
    background-color: lightcoral;
    text-align: center;
    font-size: large;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
  }

  .winner {
    background-color: #3fd14b;
  }
</style>