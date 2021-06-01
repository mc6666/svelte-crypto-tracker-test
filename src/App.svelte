<script>
	// export let name;
    let name = 'michael';
    
    import CoinCard from "./CoinCard.svelte"
    
    let coins = [];

    async function fetchCoins() {
    const response = await fetch(
      "https://api.coinstats.app/public/v1/coins?skip=0&limit=20"
    );
    const data = await response.json();
    coins = data.coins;
    console.log("coins:", coins);
    }
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>

    {#if coins.length === 0}
        <button on:click={fetchCoins}>Fetch Coin Data!</button>
    {:else}
        <div class="grid">
            {#each coins as coin}
            <CoinCard {coin} />
            {/each}
        </div>
    {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 40px 0;
    margin: 0 auto;
  }
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
  }

  @media (min-width: 640px) {
    main {
      max-width: 1600px;
      padding: 40px 20px;
    }
  }
</style>