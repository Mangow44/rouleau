<script>
	import Element from './Element.svelte';

	let htmlRouleau = null;
	let list = [
		{ name: 'Test', up: 1, down: 5 },
		{ name: 'Là le texte est plus long', up: 1, down: 5 },
		{ name: 'Oui', up: 6, down: 5 },
		{ name: "Ici aussi d'ailleurs, c'est plutôt marrant", up: 1, down: 1 },
		{ name: 'Test', up: 1, down: 5 },
		{ name: 'Là le texte est plus long', up: 1, down: 5 },
		{ name: 'Oui', up: 6, down: 5 },
		{ name: "Ici aussi d'ailleurs, c'est plutôt marrant", up: 1, down: 1 },
		{ name: 'Test', up: 1, down: 5 },
		{ name: 'Là le texte est plus long', up: 1, down: 5 },
		{ name: 'Oui', up: 6, down: 5 },
		{ name: "Ici aussi d'ailleurs, c'est plutôt marrant", up: 1, down: 1 },
		{ name: 'Test', up: 1, down: 5 },
		{ name: 'Là le texte est plus long', up: 1, down: 5 },
		{ name: 'Oui', up: 6, down: 5 },
		{ name: "Ici aussi d'ailleurs, c'est plutôt marrant", up: 1, down: 1 },
		{ name: 'Test', up: 1, down: 5 },
		{ name: 'Là le texte est plus long', up: 1, down: 5 },
		{ name: 'Oui', up: 6, down: 5 },
		{ name: "Ici aussi d'ailleurs, c'est plutôt marrant", up: 1, down: 1 },
		{ name: 'Test', up: 10, down: 5 },
		{ name: 'Là le texte est plus long', up: 1, down: 5 },
		{ name: 'Oui', up: 6, down: 5 },
		{ name: "Ici aussi d'ailleurs, c'est plutôt marrant", up: 1, down: 1 }
	];

	list.sort((a, b) => {
		return b.up - b.down - (a.up - a.down);
	});
</script>

<div
	bind:this={htmlRouleau}
	class="rouleau flex flex-col 
		m-auto w-screen h-screen 
		overflow-y-auto overflow-x-hidden shrink-0"
>
	{#if htmlRouleau}
		{#each list as el}
			<Element {el} bind:htmlRouleau />
		{/each}
	{/if}
</div>

<style>
	.rouleau::before {
		position: fixed;
		pointer-events: none;
		z-index: 1;
		top: 0;
		content: '';
		width: 100vw;
		height: 10%;
		background: rgb(255, 255, 255);
		background: linear-gradient(0deg, rgba(255, 255, 255, 0) 0%, rgba(0, 0, 0, 1) 100%);
	}

	.rouleau::after {
		position: fixed;
		pointer-events: none;
		z-index: 1;
		bottom: 0;
		content: '';
		width: 100vw;
		height: 10%;
		background: rgb(255, 255, 255);
		background: linear-gradient(180deg, rgba(255, 255, 255, 0) 0%, rgba(0, 0, 0, 1) 100%);
	}

	/* Hide scrollbar for IE, Edge and Firefox */
	.rouleau {
		-ms-overflow-style: none;
		scrollbar-width: none;
	}

	/* Hide scrollbar for Chrome, Safari and Opera */
	.rouleau::-webkit-scrollbar {
		display: none;
	}
</style>
