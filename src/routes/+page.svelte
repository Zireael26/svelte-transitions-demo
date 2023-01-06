<script lang="ts">
	import { tweened } from 'svelte/motion';
	import { sineInOut } from 'svelte/easing';
	// import Spring from './Spring.svelte';
	import { blur, fade, fly, scale, slide } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	const progress = tweened(0, {
		delay: 0,
		duration: 750,
		easing: sineInOut
	});

	setTimeout(() => {
		progress.set(50);
	}, 2000);

	let boxInput = '';
	let boxes: Array<string> = [];

	function addBox() {
		boxes = [boxInput, ...boxes];
		boxInput = '';
	}

	function discard(boxValue: string) {
		boxes = boxes.filter((box) => box !== boxValue);
	}
</script>

<!-- <progress max="100" value={$progress} /> -->
<!-- <Spring /> -->
<input type="text" bind:value={boxInput} />
<button on:click={addBox}>Add Box</button>

{#each boxes as box (box)}
	<div
		class="box"
		in:fly={{
			x: 200,
			y: 0
		}}
		out:fly={{
			x: -200,
			y: 0
		}}
		on:click={discard.bind(this, box)}
		on:keypress
		animate:flip={{ duration: 500 }}
	>
		{box}
	</div>
{/each}

<style>
	div {
		width: 10rem;
		height: 10rem;
		background-color: #ccc;
		margin: 1rem;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		border-radius: 5px;
		padding: 1rem;
	}
</style>
