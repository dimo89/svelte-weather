<script>
  export let clouds;
  export let visibility;
</script>

<style>
  div {
    color: #a2d3cb;
    text-transform: uppercase;
		font-size: 1.2em;
    font-weight: 300;
    line-height: 1.4em;
  }
</style>

<div style="margin-top: 20px">
  <div>Clouds: {clouds.all}%</div>
  <div>Visibility: {visibility}m</div>
</div>