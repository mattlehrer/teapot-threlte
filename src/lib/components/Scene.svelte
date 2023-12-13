<script lang="ts">
	import { OrbitControls } from '@threlte/extras';
	import { T } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { useLoader } from '@threlte/core';
	import { OBJLoader } from 'three/addons/loaders/OBJLoader.js';

	const model = useLoader(OBJLoader).load('/teapot.obj');

	interactivity();
</script>

<T.PerspectiveCamera
	makeDefault
	position={[10, 10, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 1, 0);
	}}
>
	<OrbitControls enableDamping autoRotate />
</T.PerspectiveCamera>

{#if $model}
	<T is={$model} />
{/if}

<T.AmbientLight intensity={0.25} />
<T.DirectionalLight intensity={0.5} position={[0, 10, 0]} />
