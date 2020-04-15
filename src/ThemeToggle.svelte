<script>
  import { getContext } from "svelte";
  const { theme, toggle } = getContext("theme");
</script>

<style>
  button {
    position: absolute;
    right: 20px;
    top: 20px;
  }
</style>

<button on:click={toggle}>{$theme.name}</button>
