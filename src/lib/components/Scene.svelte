<script lang="ts">
	import { OrbitControls } from '@threlte/extras';
	import { T, useTask } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { spring } from 'svelte/motion';
	import { useLoader } from '@threlte/core';
	import { OBJLoader } from 'three/addons/loaders/OBJLoader.js';

	const model = useLoader(OBJLoader).load('/teapot.obj');

	interactivity();

	let rotation = 0;
	useTask((delta) => {
		rotation += delta;
	});
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
