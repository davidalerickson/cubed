<script>
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';

	let star;
	const loader = new GLTFLoader();

	loader.load('./star.gltf', (gltf) => {
		star = gltf.scene.children[0].geometry;
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
