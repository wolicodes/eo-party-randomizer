<script>
  import GameSelect from "./GameSelect.svelte";
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
    console.log('classes', classes)
  };

  const handleGameChanged = event => {
    game = event.detail.game;
    refreshClasses();
  };

  const handleUnlockableChanged = () => {
    refreshClasses();
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
  <GameSelect selected={game} on:selectgame={handleGameChanged} />

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
        on:change={handleUnlockableChanged} />
    </p>
    <button type="submit">Randomize</button>
  </form>

  <div id="party">{party.join(' / ')}</div>
</main>
