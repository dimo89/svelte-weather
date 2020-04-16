<script>
  import City from "./City.svelte";
  import Weather from "./Weather.svelte";
  import Wind from "./Wind.svelte";
  import Clouds from "./Clouds.svelte";
  import Description from "./Description.svelte";
  import ThemeToggle from "./ThemeToggle.svelte";
  import ThemeContext from "./ThemeContext.svelte";
  import GetForecastButton from "./GetForecastButton.svelte";

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
  :global(html) {
    background-color: var(--theme-background);
    color: var(--theme-text);
    transition: background-color 200ms linear;
  }

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
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
<ThemeContext>
  <main>
    <GetForecastButton on:click={handleClick} />
    <ThemeToggle />
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
</ThemeContext>
