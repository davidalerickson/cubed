<script>
	import { onMount } from 'svelte';
	import * as SC from 'svelte-cubed';
	import { FontLoader } from 'three/examples/jsm/loaders/FontLoader.js';
	import { TextGeometry } from 'three/examples/jsm/geometries/TextGeometry.js';
	import typeface from '@compai/font-mako/data/typefaces/mako-normal-400.json';
	let text = 'Hello, world!';
	let font;
	let loader = new FontLoader();

	onMount(() => {
		font = loader.parse(typeface);
	});
</script>

<div class="controls">
	<input type="text" bind:value={text} />
</div>

<SC.Canvas antialias alpha>
	<SC.Mesh
		geometry={new TextGeometry(text, {
			font: font,
			size: 16,
			height: 0.2,
			bevelEnabled: true,
			bevelOffset: 0,
			bevelSegments: 32,
			bevelSize: 1,
			bevelThickness: 4
		})}
	/>
	<SC.PerspectiveCamera position={[10, 0, 100]} />
	<SC.AmbientLight />
	<SC.OrbitControls />
</SC.Canvas>

<style>
	.controls {
		position: absolute;
		z-index: 10;
	}
</style>
