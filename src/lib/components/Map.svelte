<script>
	import { Deck } from "@deck.gl/core";
	import { onMount } from "svelte";

	export let latitude = 0;
	export let longitude = 0;
	export let zoom = 0;

	export let layers = [];

	let container;
	let canvas;
	let deck;

	onMount(() => {
		deck = new Deck({
			parent: container,
			canvas,
			initialViewState: {
				longitude,
				latitude,
				zoom
			},
			controller: true,
			layers
		});
	});

	$: layers, deck && deck.setProps({ layers });
</script>

<div id="container" bind:this={container}>
	<canvas bind:this={canvas} />
</div>
