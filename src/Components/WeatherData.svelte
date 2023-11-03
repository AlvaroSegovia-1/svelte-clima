<script lang="ts">
  export let weather: any;
</script>

<div class="max-w-none flex flex-wrap justify-center">
  <div class="min-w-fit animate__animated animate__fadeInUp basis-1/3 m-6">
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
      City: <span class="font-bold">{weather.name}, {weather.sys.country}</span>
    </h4>
    <h4>
      Weather: <span class="font-bold">{weather.weather[0].description}</span>
    </h4>
  </div>
  <div
    class=" min-w-fit animate__animated animate__fadeInUp basis-1/3 w-20 m-6"
  >
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
</div>
