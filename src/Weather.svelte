<script>
  export let temp;
  export let temp_max;
  export let temp_min;
  export let feels_like;
  export let pressure;
  export let humidity;

  function kelvitToCelsius(kelvin) {
    return (kelvin - 273.15).toFixed(1);
  }
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

<div>
  <div>Temperature: {kelvitToCelsius(temp)}˚C</div>
  <div>Max/min: {kelvitToCelsius(temp_max)}/{kelvitToCelsius(temp_min)}˚C</div>
  <div>Feels like: {kelvitToCelsius(feels_like)}˚C</div>
  <div>Pressure: {pressure}hPa</div>
  <div>Humidity: {humidity}%</div>
</div>