<script>
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';
	import * as PE from 'svelte-cannon';
	import Box from '$lib/Box.svelte';

	let count = 1;
	$: console.log(count);
</script>

<button class="controls" on:click={() => count++}>More Boxes</button>
<!-- <svelte:window on:click={() => count++} /> -->

<PE.World gravity={[0, -9.8, 0]}>
	<SC.Canvas antialias shadows>
		<PE.Body mass={0} rotation={[-Math.PI / 2, 0, 0]}>
			<PE.Plane />
		</PE.Body>
		<SC.Mesh
			geometry={new THREE.PlaneGeometry(50, 50)}
			rotation={[-Math.PI / 2, 0, 0]}
			material={new THREE.MeshStandardMaterial({ color: 'grey' })}
			receiveShadow
		/>

		{#each { length: count } as _}
			<Box />
		{/each}

		<SC.PerspectiveCamera position={[2, 2, 15]} target={[0, 0, 0]} />
		<SC.OrbitControls />
		<SC.DirectionalLight intensity={1} position={[15, 15, 15]} shadow={{ mapSize: [2048, 2048] }} />
		<SC.AmbientLight intensity={1} />
	</SC.Canvas>
</PE.World>

<style>
	.controls {
		position: absolute;
		z-index: 10;
		bottom: 20px;
		right: 50%;
		transform: translateX(50%);
	}
</style>
