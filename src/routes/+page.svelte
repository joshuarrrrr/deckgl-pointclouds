<script>
	import Map from "$lib/components/Map.svelte";
	import { COORDINATE_SYSTEM } from "@deck.gl/core";
	import { PointCloudLayer } from "@deck.gl/layers";

	let color = [0, 0, 0];

	setInterval(() => {
		color = [Math.random() * 255, Math.random() * 255, Math.random() * 255];
	}, 1000);

	$: layers = [
		new PointCloudLayer({
			id: "PointCloudLayer",
			data: "https://raw.githubusercontent.com/visgl/deck.gl-data/master/website/pointcloud.json",
			getColor: color,
			getNormal: (d) => d.normal,
			getPosition: (d) => d.position,
			pointSize: 2,
			coordinateOrigin: [-122.4, 37.74],
			coordinateSystem: COORDINATE_SYSTEM.METER_OFFSETS,
			pickable: false
		})
	];
</script>

<Map longitude={-122.4} latitude={37.74} zoom={11} {layers} />
