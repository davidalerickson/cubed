<script>
	import { onMount } from 'svelte';
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import { SVGLoader } from 'three/examples/jsm/loaders/SVGLoader.js';
	import logo from '$lib/logo.svg?raw';

	const svgLogo = new SVGLoader().parse(logo);
	console.log(svgLogo);
</script>

<!-- <div class="controls">
	<input type="range" bind:value={text} />
</div> -->

<SC.Canvas antialias alpha>
	<SC.Group scale={0.05} rotation={[Math.PI, 0, 0]}>
		{#each svgLogo.paths as logoPath}
			<SC.Mesh
				geometry={new THREE.ExtrudeGeometry(logoPath.toShapes(false), {
					depth: 40
				})}
			/>
		{/each}
	</SC.Group>
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
