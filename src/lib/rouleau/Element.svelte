<script>
	import { onMount } from 'svelte';

	export let el = '';
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
			console.log(htmlRouleau.scrollTop);
			updateRotation();
		});
		window.addEventListener('resize', () => {
			updateRotation();
		});
	});

	$: console.log(hover);
</script>

<div
	bind:this={htmlDiv}
	class=" flex items-center 
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
		class="w-full px-[0.5rem] 
			cursor-pointer smooth overflow-hidden
			text-[3.3rem] stroke text-transparent font-medium whitespace-nowrap text-ellipsis 
			{hover ? 'scale-105 translate-x-[2.5rem]' : ''}"
	>
		{el}
	</p>
	<!-- GO FIGMA faire tuc haut bas et implémenter le nombre -->
	<span class="smooth bg-violet-300 w-[20%] h-full {hover ? 'scale-120 translate-x-[2.7rem]' : ''}">
		ok</span
	>
</div>

<style>
	.smooth {
		transition: all 0.5s ease;
	}

	.stroke {
		-webkit-text-stroke-width: 1px;
		-webkit-text-stroke-color: white;
	}

	.stroke:hover {
		color: white;
	}
</style>
