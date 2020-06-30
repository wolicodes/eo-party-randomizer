<script>
  import classesData from "./classes.json";

  let party = [];
  let nbMembers = 5;
  let noDupes = false;
  let unlockable = false;
  let game = "eon";
  let classes = classesData[game].classes;

  const refreshClasses = () => {
    classes = classesData[game].classes;
    if (unlockable) {
      classes = classes.concat(classesData[game].unlockable);
    }
  };

  const handleSubmit = () => {
    party = [];

    if (isNaN(nbMembers)) {
      return;
    }

    for (let i = 0; i < nbMembers; i++) {
      let character = classes[Math.floor(Math.random() * classes.length)];
      while (noDupes && party.indexOf(character) !== -1) {
        character = classes[Math.floor(Math.random() * classes.length)];
      }
      party.push(character);
    }
  };
</script>

<style>
  #party {
    margin-top: 20px;
  }
</style>

<main>
    <p>
      Choose your game
      <select bind:value={game} on:blur={refreshClasses}>
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

  <form on:submit|preventDefault={handleSubmit}>
    <p>
      <label for="nb-members">How many party members?</label>
      <input
        id="nb-members"
        type="number"
        bind:value={nbMembers}
        min="1"
        max="5" />
    </p>
    <p>
      <label for="no-dupes">No duplicate class</label>
      <input id="no-dupes" type="checkbox" bind:checked={noDupes} />
    </p>
    <p>
      <label for="unlockable-classes">Include unlockable classes</label>
      <input
        id="unlockable-classes"
        type="checkbox"
        bind:checked={unlockable}
        on:change={refreshClasses} />
    </p>
    <button type="submit">Randomize</button>
  </form>

  <div id="party">{party.join(' / ')}</div>
</main>
