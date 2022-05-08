<script>
	import * as PE from "svelte-cannon";
	import * as THREE from "three";
	import * as SC from "svelte-cubed";
	const position = PE.writableVec3(0, 6, 0);
</script>

<PE.Body mass={1} bind:position={$position}>
	<PE.Sphere radius={1} />
</PE.Body>

<SC.Mesh
  position={$position.toArray()}
	geometry={new THREE.SphereGeometry()}
	material={new THREE.MeshStandardMaterial({ color: '#FF7F50' })}
	castShadow
	receiveShadow
/>
