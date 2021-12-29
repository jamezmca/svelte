<script>
	import { fade, fly } from "svelte/transition";
	import { randomStore } from "./store";
	import Child from './Child.svelte'
	//randomStore.set or update
	//randomStore.update((v) => v + 1); //gives current value
	//randomStore.subscribe(v => ...) need to manage subscriptions carefully
	let data = {
		userId: 123456,
		name: 'james',
		email: 'banana@bananac.om'
	}
	export let name;
	let rando;
	$: result = Math.round(rando * 100);
	let randos = [];
	function setRando() {
		rando = Math.random();
		randos = [...randos, rando]; //instead of .push(rando) as svlete is reactive to assignment
	}

	function delay(ms) {
		return new Promise((resolve) => setTimeout(resolve, ms));
	}
	let rando2 = delay(2000).then((v) => Math.random());
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>
		Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
		how to build Svelte apps.
	</p>
	<Child userId={data.userId} name={data.name} email={data.email}/>
	<Child {...data}/>
	<h1>Rando is {result}</h1>
	<button on:click={setRando}>Randomize</button>
	<input bind:value={rando} />

	{#if result > 75}
		<p transition:fade>fat</p>
	{:else if result > 50}
		<p
			in:fly={{ x: 1000, duration: 500 }}
			out:fly={{ x: -500, duration: 500 }}
		>
			tiddies
		</p>
	{:else}
		<p>loser</p>
	{/if}
	<hr />
	<!-- {$randomStore} subscribes to it -->
	{$randomStore}
	<button on:click={() => randomStore.set(Math.random())}>Siiiccckk</button>

	{#await rando2}
		<p>thinking about it...</p>
	{:then number}
		<p>number: {number}</p>
	{:catch error}
		<p>{error.message}</p>
	{/await}

	<ul>
		{#each randos as val, idx}
			<p>{val}</p>
		{/each}
	</ul>
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
