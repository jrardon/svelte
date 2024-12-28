<script>
  import Character from "./lib/Character.svelte";

  let characters = [];
  let page = 1;

  async function loadCharacter() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page,
    );
    const data = await response.json();
    characters = data.results;
  }

  loadCharacter();

  function nextPage() {
    page++;
    loadCharacter();
  }

  function previousPage() {
    page--;
    loadCharacter();
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1>

<div class="container">
  <div class="btns">
    <button class="btn" on:click={previousPage} disabled={page == 1}>previous</button>
    <button class="btn" on:click={nextPage}>next</button>
  </div>
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
