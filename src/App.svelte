<script>
	import { fade, fly } from "svelte/transition";

	let rando = Math.round(Math.random() * 100);
	let generated = 1;
	let randos = [rando];
	function setRando() {
		rando = Math.round(Math.random() * 100);
		let heading = document.getElementById("heading");
		let color = "#" + Math.floor(Math.random() * 16777215).toString(16);
		console.log(color);
		heading.style.color = color;
		generated += 1;
		randos = [...randos, rando];
	}
</script>

<main>
	<h1 id="heading">Random Number Generator</h1>
	<p><span> Number Generated is {rando}</span></p>
	{#if rando > 75}
		<p>Top 25%! 🎉</p>
	{:else if rando > 50}
		<p>Atleast 50%. 🙂</p>
	{:else}
		<p>Less than 50% 😪</p>
	{/if}
	<p>Generated Yet: {generated}</p>
	<button on:click={setRando}>Randomize Number</button>
	<div>
		<p>Numbers generated yet are:</p>
		{#each randos as num}
			<span transition:fade={{
				delay: 100,
				duration: 300
			}}> {num} </span>
		{/each}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #611b8f;
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
