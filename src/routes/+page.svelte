<script>
	import Map from "$lib/components/Map.svelte";
	import { COORDINATE_SYSTEM } from "@deck.gl/core";
	import { PointCloudLayer } from "@deck.gl/layers";
	import { onMount } from "svelte";

	let n = 9;
	let visible = Array(n).fill(true);

	onMount(() => {
		// run this function in regular intervals
		const timer = setInterval(() => {
			visible = Array.from({ length: n }, () => Math.random() > 0.5);
		}, 1000);

		// clear the interval when this component is destroyed
		return () => clearInterval(timer);
	});

	$: layers = visible.map(
		(visible, index) =>
			new PointCloudLayer({
				id: `PointCloudLayer${index}`,
				visible,
				data: "https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/pointcloud.json",
				getColor: (d) => d.color,
				getNormal: (d) => d.normal,
				getPosition: (d) => d.position,
				pointSize: 2,
				coordinateOrigin: [-122.6 + index * 0.05, 37.74],
				coordinateSystem: COORDINATE_SYSTEM.METER_OFFSETS,
				pickable: false
			})
	);
</script>

<Map longitude={-122.4} latitude={37.74} zoom={11} {layers} />
