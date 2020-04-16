<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function onClick() {
    dispatch("click", {});
  }
</script>

<style>
  button {
    outline: none;
    border-radius: 12px;
    color: #a2aad3;
    background-color: var(--theme-background);
    border: 1px solid #a2aad3;
    padding: 6px 12px;
    text-transform: uppercase;
    font-weight: 300;
    transition: background-color 200ms linear;
  }

  button:hover {
    cursor: pointer;
    color: #8188a8;
    border: 1px solid#8188a8;
  }
</style>

<button on:click={onClick}>Get Forecast</button>
