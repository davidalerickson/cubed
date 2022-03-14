<script>
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import { spring } from 'svelte/motion';
	let width = 1;
	let height = 1;
	let depth = 1;

	let spin = 0;

	let isActive = false;

	let xPos = spring(0);
	$: $xPos = isActive ? 10 : 0;

	SC.onFrame(() => {
		spin += 0.01;
	});
</script>

<svelte:window
	on:click={() => {
		isActive = !isActive;
	}}
/>

<div class="controls">
	<label>Width:<input type="range" min={0.1} max={3} step={0.1} bind:value={width} /> </label>
	<label>Height:<input type="range" min={0.1} max={3} step={0.1} bind:value={height} /> </label>
	<label>Depth:<input type="range" min={0.1} max={3} step={0.1} bind:value={depth} /> </label>
</div>

<SC.Canvas antialias background={new THREE.Color('white')}>
	<SC.Mesh
		position={[$xPos, 0, 0]}
		scale={[width, height, depth]}
		rotation={[0, spin, 0]}
		material={new THREE.MeshStandardMaterial({ color: 'red' })}
		geometry={new THREE.BoxGeometry()}
	/>
	<SC.PerspectiveCamera position={[2, 2, 2]} />
	<SC.OrbitControls />
	<SC.AmbientLight intensity={0.5} />
	<SC.DirectionalLight intensity={0.7} position={[3, 5, 4]} />
</SC.Canvas>

<style>
	.controls {
		position: absolute;
		z-index: 10;
	}
	label {
		display: block;
	}
</style>
