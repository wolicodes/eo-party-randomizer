<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let selected;

  const handleChange = event => {
    dispatch("selectgame", {
      game: selected
    });
  };
</script>

<style>

</style>

<p>
  Choose your game
  <select bind:value={selected} on:blur={handleChange}>
    <option value="eo1">Etrian Odyssey</option>
    <option value="eo2">Etrian Odyssey II</option>
    <option value="eo3">Etrian Odyssey III</option>
    <option value="eo4">Etrian Odyssey IV</option>
    <option value="eou">Etrian Odyssey Untold</option>
    <option value="eou2">Etrian Odyssey Untold 2</option>
    <option value="eo5">Etrian Odyssey V</option>
    <option value="eon">Etrian Odyssey Nexus</option>
  </select>
</p>