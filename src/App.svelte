<script>
	export let name;
	let rando;
	$: result = Math.round(rando) ? "winner" : "loser";

	function setRando() {
		rando = Math.random();
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>
		Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
		how to build Svelte apps.
	</p>

	<h1>Rando is {result}</h1>
	<button on:click={setRando}>Randomize</button>
	<input bind:value={rando} />

	{#if result > 75}
		<p>fat</p>
	{:else if result > 50}
		<p>tiddies</p>
	{:else}
		<p>loser</p>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
