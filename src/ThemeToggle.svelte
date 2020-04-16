<script>
  import { getContext } from "svelte";
  const { theme, toggle } = getContext("theme");
</script>

<style>
  .toggle {
    position: absolute;
    right: 20px;
    top: 20px;
    display: flex;
    align-items: center;
  }

  span {
    font-size: 20px;
    margin: 0 5px;
  }

  input[type="checkbox"] {
    height: 0;
    width: 0;
    visibility: hidden;
  }

  label {
    cursor: pointer;
    text-indent: -9999px;
    width: 54px;
    height: 28px;
    background: #27323a;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 100px;
    position: relative;
  }

  label:after {
    content: "";
    background: var(--theme-background);
    width: 22px;
    height: 22px;
    border-radius: 50%;
    position: absolute;
    top: 3px;
    left: 4px;
    transition: ease-in-out 200ms;
  }

  input:checked + label {
    background: var(--theme-text);
  }

  input:checked + label:after {
    left: calc(100% - 4px);
    transform: translateX(-100%);
  }
</style>

<div class="toggle">
  <span>🌙</span>
  <input
    class="toggle-switch"
    type="checkbox"
    id="toggle-switch"
    name="mode"
    on:click={toggle} />
  <label for="toggle-switch">
    <span class="screen-reader-text">Toggle Color Scheme</span>
  </label>
  <span>☀️</span>
</div>
