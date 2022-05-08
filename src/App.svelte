<script>
  import * as THREE from "three";
  import * as SC from "svelte-cubed";
  import * as PE from "svelte-cannon";
  import Cube from "./components/Cube.svelte"
  import Sphere from "./components/Sphere.svelte"

  let cubeCount = 1 
  let sphereCount = 0 

  // spawn cube function
  function spawnCube() {
	  cubeCount++
  }
  function spawnSphere() {
	  sphereCount++
  }
</script>

<div class="buttonDiv">
	<button on:click={spawnCube}>
		Spawn cube
	</button>
	<button on:click={spawnSphere}>
		Spawn sphere
	</button>
</div>

<PE.World gravity={[0, -9.81,0 ]}>
<SC.Canvas
	antialias
	background={new THREE.Color('white')}
	fog={new THREE.FogExp2('papayawhip', 0.001)}
  	shadows={THREE.PCFSoftShadowMap}
>
		{#each {length: cubeCount} as _}
			<Cube />
		{/each}

		{#each {length: sphereCount} as _}
			<Sphere />
		{/each}

		<!-- Ground -->
		<PE.Body mass={0} rotation={[-Math.PI / 2, 0, 0]}>
			<PE.Plane />
		</PE.Body>
   	 	<SC.Mesh
			geometry={new THREE.PlaneGeometry(20, 20)}
			material={new THREE.MeshStandardMaterial({ color: '#FFE5B3' })}
			rotation={[-Math.PI / 2, 0, 0]}
			receiveShadow
		/>
		<!-- Scene setup -->
    	<SC.PerspectiveCamera position={[2, 2, 15]} target={[0,2,0]}/>
		<SC.OrbitControls  maxPolarAngle={Math.PI * 0.49} />
		<SC.AmbientLight intensity={0.2} />
		<SC.DirectionalLight intensity={0.8} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
		<SC.HemisphereLight intensity={0.2}/>
	</SC.Canvas>
</PE.World>

<style>
.buttonDiv {
	position: absolute;
	top: 0;
	left: 0;
	z-index: 1;
}	
</style>