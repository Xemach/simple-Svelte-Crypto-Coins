<script>
	import CoinCard from "./CoinCard.svelte";
	let coins = [];
	let name = 'CRYPTO COINS'
	async function getCoins() {
		const responsePromise = await fetch("https://api.coinstats.app/public/v1/coins?skip=0&limit=20")
		const data = await responsePromise.json();
		coins = data.coins;
		console.log(coins)
	}

</script>

<main>
	<h1>{name}</h1>
	{#if coins.length === 0}
		<button on:click={getCoins}>Fetch Coin Data!</button>
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