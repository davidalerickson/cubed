<script>
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader';

	let star;
	const loader = new OBJLoader();

	loader.load('./cornellbox.obj', (obj) => {
		console.log(obj);
		scene.add(obj);
	});
</script>

<SC.Canvas antialias alpha>
	<SC.Mesh geometry={star} />
	<SC.PerspectiveCamera position={[15, 15, 15]} />
	<SC.OrbitControls />
	<SC.AmbientLight intensity={0.5} />
	<SC.DirectionalLight intensity={0.7} position={[3, 5, 4]} />
</SC.Canvas>

<style>
	.controls {
		position: absolute;
		z-index: 10;
	}
</style>
