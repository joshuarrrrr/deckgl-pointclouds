<script>
	import Map from "$lib/components/Map.svelte";
	import { ScatterplotLayer } from "@deck.gl/layers";

	let color = [0, 0, 0];

	setInterval(() => {
		color = [Math.random() * 255, Math.random() * 255, Math.random() * 255];
	}, 1000);
</script>

<Map
	zoom={15}
	layers={[
		new ScatterplotLayer({
			data: [{ position: [0, 0], color, radius: 100 }],
			getColor: (d) => d.color,
			getRadius: (d) => d.radius
		})
	]}
/>
