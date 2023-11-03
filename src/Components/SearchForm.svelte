<script lang="ts">
  export let handleSubmit: (city: string) => void;
  export let city: string;
</script>

<form on:submit|preventDefault={() => handleSubmit(city)}>
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
