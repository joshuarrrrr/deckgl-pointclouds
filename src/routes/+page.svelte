<script>
	import Deck from "$lib/components/Deck.svelte";
	import { COORDINATE_SYSTEM } from "@deck.gl/core";
	import { PointCloudLayer } from "@deck.gl/layers";
	import { onMount } from "svelte";

	let n = 9;
	const randomVisibility = () => Array.from({ length: n }, () => Math.random() > 0.2);
	let visible = randomVisibility();

	onMount(() => {
		// run this function in regular intervals
		const timer = setInterval(() => {
			visible = randomVisibility();
		}, 1000);

		// clear the interval when this component is destroyed
		return () => clearInterval(timer);
	});

	// reactively (re-)create the layers array
	$: layers = visible.map(
		(visible, index) =>
			new PointCloudLayer({
				id: `PointCloudLayer${index}`,
				visible,
				data: [{ position: [0, 0, 0] }],
				getColor: [255, 0, 0],
				getPosition: (d) => d.position,
				pointSize: 1000,
				sizeUnits: "meters",
				coordinateOrigin: [-122.6 + index * 0.05, 37.74],
				coordinateSystem: COORDINATE_SYSTEM.METER_OFFSETS,
				pickable: false
			})
	);
</script>

<Deck longitude={-122.4} latitude={37.74} zoom={11} {layers} />
