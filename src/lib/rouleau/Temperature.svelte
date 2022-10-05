<script>
	export let el = {};
	export let hover = false;

	let selected = 'lukewarm';

	function setSelected() {
		if (el.up == el.down) return;
		if (el.up > el.down) {
			selected = 'warm';
		} else {
			selected = 'cold';
		}
	}

	setSelected();
</script>

<span class="relative flex w-[5rem] h-full shrink-0">
	{#if selected == 'warm'}
		<img
			class="m-auto object-contains h-auto w-[40%] smooth {hover ? 'scale-150' : ''}"
			src="/fire-svgrepo-com.svg"
			alt="fire"
		/>
	{:else if selected == 'lukewarm'}
		<img
			class="m-auto object-contains h-auto w-[40%] smooth {hover ? 'scale-150' : ''}"
			src="/fire-svgrepo-com.svg"
			alt="fire"
		/>
	{:else if selected == 'cold'}
		<img
			class="m-auto object-contains h-auto w-[40%] smooth {hover ? 'scale-150' : ''}"
			src="/snowflake-svgrepo-com.svg"
			alt="snowflake"
		/>
	{/if}
</span>
