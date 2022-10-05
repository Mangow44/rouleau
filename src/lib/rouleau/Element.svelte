<script>
	import { onMount } from 'svelte';
	import Temperature from './Temperature.svelte';

	export let el = {};
	export let htmlRouleau = null;

	let htmlDiv = null;
	let htmlText = null;
	let hover = false;

	onMount(() => {
		const updateRotation = () => {
			if (!htmlDiv) return;
			let dist =
				htmlRouleau.clientHeight / 2 -
				(htmlDiv.getBoundingClientRect().y + htmlDiv.clientHeight / 2 - htmlRouleau.offsetTop);
			let distCube = dist * dist * dist * 2;
			let factor = 1 * 155 ** 3.2;
			htmlDiv.style.transform =
				'skewX(' +
				distCube / factor +
				'deg) rotateX(' +
				distCube / factor +
				'deg) translateX(' +
				(10 - Math.abs((distCube / factor) * 2)) +
				'px)';
		};

		updateRotation();

		htmlRouleau.addEventListener('scroll', () => {
			updateRotation();
		});

		window.addEventListener('resize', () => {
			updateRotation();
		});
	});
</script>

<div
	bind:this={htmlDiv}
	class=" flex items-center cursor-pointer
		m-auto w-full h-auto
		px-[1rem] shrink-0"
	on:focus={() => console.log('focus')}
	on:mouseover={() => {
		hover = true;
	}}
	on:mouseleave={() => {
		hover = false;
	}}
>
	<p
		bind:this={htmlText}
		class="w-full pr-[2rem]
			smooth overflow-hidden
			text-[3.3rem] stroke text-transparent font-medium whitespace-nowrap text-ellipsis 
			{hover ? 'translate-x-[1rem] scale-105 stroke-color' : ''}"
	>
		{el.name}
	</p>

	<Temperature bind:el bind:hover />
</div>

<style>
	.stroke {
		-webkit-text-stroke-width: 1px;
		-webkit-text-stroke-color: white;
	}

	.stroke-color {
		color: white;
	}
</style>
