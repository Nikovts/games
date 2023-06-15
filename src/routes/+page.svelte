<script lang="ts">
  // Importing the required components and data from external files
  import Tabs from "../lib/Tabs.svelte";
  import Card from "../lib/Card.svelte";
  import { gamesData, developers, type } from "../store.js";
  import type { IGameData, TypeTabs } from "../store.js";


  // Initializing variables
  let games: IGameData[] = $gamesData;
  let availableDevelopers: TypeTabs[] = $developers;
  let selectedDevs: number = -1;
  let currentTypeGames: IGameData[] = $gamesData;

  // Event handler for when a game type is selected
  function handleTypeSelected(event: any) {
    selectedDevs = -1;

    // Check if the selected type is "All"
    if (event.detail.title === "All") {
      games = $gamesData;
      currentTypeGames = $gamesData;
      availableDevelopers = $developers;
    } else {
      // Filter games based on the selected type
      let gameType = event.detail.title.toLowerCase();
      games = $gamesData.filter((game) => Object.hasOwn(game, gameType));

      // Update available developers based on filtered games
      availableDevelopers = $developers.filter((dev) =>
        games.some((game) => game.developer === dev.title)
      );
    }

    currentTypeGames = games;
  };


  // Event handler for when a developer is selected
  function handleDeveloperSelected(event: any) {
    selectedDevs = event.detail.index;

    // Filter games based on the selected developer
    games = currentTypeGames.filter(
      (game) => game.developer === event.detail.title
    );
  }
</script>

<!-- Main section -->
<div class="main">
  <!-- Display game type tabs -->
  <Tabs
    tabs={$type}
    row={true}
    selected="0"
    on:tabSelected={handleTypeSelected}
  />

  <!-- Display developer tabs -->
  <Tabs
    tabs={availableDevelopers}
    row={false}
    selected={selectedDevs}
    on:tabSelected={handleDeveloperSelected}
  />

  <!-- Display game cards -->
  <section class="games">
    {#each games as game}
      <Card {game} />
    {/each}
  </section>
</div>


<style lang="scss">
  .main {
    font-family: "Lato", sans-serif;
    background: #ffffff;
    border-radius: 20px;
    padding: 150px 120px 0 120px;
    width: max-content;
    margin: auto;
    .games {
      display: grid;
      grid-template-columns: repeat(4, minmax(304px, 304px));
      gap: 19px;
      margin-top: 20px;
      @media screen and (max-width: 1540px) {
        grid-template-columns: repeat(3, minmax(304px, 304px));
      }
      @media screen and (max-width: 1220px) {
        grid-template-columns: repeat(2, minmax(304px, 304px));
      }
    }
  }
</style>
