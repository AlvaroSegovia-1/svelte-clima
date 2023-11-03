<script lang="ts">
  import ErrorAlert from "./ErrorAlert.svelte";
  import Loading from "./Loading.svelte";
  import SearchForm from "./SearchForm.svelte";
  import WeatherData from "./WeatherData.svelte";

  const APIKEY = "b5caee92e26468eb94536a52fb0bc0ad";
  let city = "";

  const getWeatherData = async (city: string = "mexico") => {
    const baseUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&APPID=${APIKEY}`;

    if (city.trim() === "") {
      throw new Error("Name invalid or empty");
    }

    const res = await fetch(baseUrl);

    const data = await res.json();

    console.log(data);

    if (data.cod == "404") {
      throw new Error("This name don´t exist");
    }

    return data;
  };

  let promise = getWeatherData();

  const handleSubmit = () => {
    promise = getWeatherData(city);
    city = "";
  };
</script>

<div
  class="container mx-auto max-h-fit max-w-fit w-4/5 mt-8 pb-20 bg-slate-300 rounded-xl"
>
  <div class="flex flex-col justify-center">
    <div class="basis-1/3 m-6">
      <form on:submit|preventDefault={() => handleSubmit()}>
        <label>
          City: <input
            bind:value={city}
            type="text"
            class=" px-2 py-1 bg-stone-300 border rounded border-black"
          />
        </label>
        <button class="m-4 py-1 px-2 bg-stone-300 border rounded border-black"
          >Search</button
        >
      </form>
    </div>

    {#await promise}
      <div class=" mt-5">
        <Loading />
      </div>
    {:then weather}
      <WeatherData {weather} />
    {:catch error}
      <div class=" mt-5">
        <ErrorAlert {error} />
      </div>
    {/await}
  </div>
</div>
