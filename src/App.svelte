<script>
	import City from "./City.svelte";
	import Weather from './Weather.svelte';
	import Wind from './Wind.svelte';
	import Clouds from './Clouds.svelte';
	import Description from './Description.svelte';

  let promise = getForecast();
  const API_KEY = "483da3075ed2856a4352900f0911b283";
  const CITY_NAME = "Tallinn";

  async function getForecast() {
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${CITY_NAME}&appid=${API_KEY}`
    );
    const data = await response.json();

    if (response.ok) {
      return data;
    } else {
      throw new Error(data);
    }

    console.log("response: ", data);
  }

  function handleClick() {
    promise = getForecast();
  }
  
	
	setInterval(handleClick, 60000);
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
	}
	
	button {
		outline: none;
    border-radius: 12px;
		color: #a2aad3;
		background-color: #ffffff;
    border: 1px solid #a2aad3;
    padding: 6px 12px;
    text-transform: uppercase;
    font-weight: 300;
	}

	button:hover {
		cursor: pointer;
		color: #8188a8;
		border: 1px solid#8188a8;
	}

	p {
		color: #a2aad3;
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<svelte:head>
  <title>Svelte Open Weather</title>
</svelte:head>
<main>
  <button on:click={handleClick}>Get Forecast</button>
  {#await promise}
    <p>loading...</p>
  {:then data}
    <City name={data.name} />
		<Description description={data.weather[0].description} />
    <Weather {...data.main} />
		<Wind {...data.wind} />
		<Clouds clouds={data.clouds} visibility={data.visibility} />
  {:catch error}
    <p style="color: #ee4c75">{error.message}</p>
  {/await}
</main>
