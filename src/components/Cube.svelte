<script>
	import * as CANNON from "cannon-es";
	import * as PE from "svelte-cannon";
	import * as THREE from "three";
	import * as SC from "svelte-cubed";
	
	const position = PE.writableVec3(0, 6, 0);
	const rnd = Math.random() * 0.1;
	let rotation = PE.writableVec3(rnd , rnd, rnd);
</script>

<PE.Body mass={1} bind:position={$position} bind:rotation={$rotation}>
	<PE.Box size={[0.5, 0.5, 0.5]} />
</PE.Body>

<SC.Mesh
	position={$position.toArray()}
	rotation={$rotation.toArray()}
	geometry={new THREE.BoxGeometry()}
	material={new THREE.MeshStandardMaterial({ color: '#FF7F50'})}
	castShadow
	receiveShadow
/>
