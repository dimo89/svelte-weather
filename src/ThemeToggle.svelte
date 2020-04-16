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

  input[type="checkbox"] {
    height: 0;
    width: 0;
    visibility: hidden;
  }

  label {
    cursor: pointer;
    text-indent: -9999px;
    width: 40px;
    height: 18px;
    background: var(--theme-switchBackground);
    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 100px;
    position: relative;
  }

  label:after {
    content: "";
    background: var(--theme-switch);
    box-shadow: 0 0 7px 1px var(--theme-switch);
    width: 22px;
    height: 22px;
    border-radius: 50%;
    position: absolute;
    left: 0px;
    transition: ease-in-out 200ms;
  }

  input:checked + label {
    background: var(--theme-switchBackground);
  }

  input:checked + label:after {
    left: 100%;
    transform: translateX(-100%);
  }
</style>

<div class="toggle">
  <input
    class="toggle-switch"
    type="checkbox"
    id="toggle-switch"
    name="mode"
    on:click={toggle} />
  <label for="toggle-switch">
    <span class="screen-reader-text">Toggle Color Scheme</span>
  </label>
</div>
