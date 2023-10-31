<script lang="ts">
  const APIKEY = "b5caee92e26468eb94536a52fb0bc0ad";
  let city = "Mexico";

  const getWeatherData = async () => {
    const res = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&APPID=${APIKEY}`
    );

    /* const res_2 = await fetch(`
    http://api.openweathermap.org/geo/1.0/direct?q=${city}&appid=${APIKEY}`); */

    const data = await res.json();

    console.log(data);

    return data;
  };

  let promise = getWeatherData();
</script>

<div class="container mx-auto mt-6">
  <div class="flex">
    {#await promise}
      Loading ...
    {:then weather}
      <div class="w-1/2">
        <div>
          <img
            class="bg-slate-300 inline-block"
            src={`http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`}
            alt={weather.name}
          />
          <h1 class="inline-block">
            {weather.main.temp}°C
          </h1>
        </div>

        <h4>
          City: <span class="font-bold"
            >{weather.name}, {weather.sys.country}</span
          >
        </h4>
        <h4>
          Weather: <span class="font-bold"
            >{weather.weather[0].description}</span
          >
        </h4>
      </div>
      <div class="w-1/2">
        <h4>
          Maximun Temperature: <span class="font-bold text-red-500"
            >{weather.main.temp_max}</span
          >
        </h4>

        <h4>
          Minimun Temperature <span class="font-bold text-blue-500"
            >{weather.main.temp_min}</span
          >
        </h4>
      </div>
    {/await}
  </div>
</div>

<!-- Apikey ed4e29db589e14003cd85cd8ee0a80fa -->
