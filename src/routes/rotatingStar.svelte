<script>
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';

	let star;
	let rotation = 0;
	const loader = new GLTFLoader();

	loader.load('./star.gltf', (gltf) => {
		star = gltf.scene.children[0].geometry;
	});

	SC.onFrame(() => {
		rotation += 0.01;
	});
</script>

<SC.Canvas antialias alpha shadows>
	<SC.Mesh
		geometry={star}
		rotation={[-90, 0, rotation]}
		material={new THREE.MeshStandardMaterial({
			color: 0xffff00,
			roughness: 0,
			metalness: 0.6
		})}
		castShadow
	/>

	<SC.Group position={[0, -2, 0]}>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(100, 100)}
			material={new THREE.MeshStandardMaterial({
				color: 'grey'
			})}
			rotation={[-Math.PI / 2, 0, 0]}
			receiveShadow
		/>
		<SC.Primitive
			object={new THREE.GridHelper(100, 100, 0x444444, 0x555555)}
			position={[0, 0.001, 0]}
		/>
	</SC.Group>
	<SC.PerspectiveCamera position={[3, 1, 3]} />
	<SC.OrbitControls />
	<SC.AmbientLight intensity={1} />
	<SC.DirectionalLight shadow={{ mapSize: [2048, 2048] }} intensity={0.7} />
	<SC.PointLight intensity={1} position={[2, 5, 2]} />
</SC.Canvas>

<style>
	.controls {
		position: absolute;
		z-index: 10;
	}
</style>
