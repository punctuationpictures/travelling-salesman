<script>
	import { onMount } from 'svelte';
	import { Canvas, T } from '@threlte/core';

	// cameras
	import Ortho from './cameras/Ortho.svelte';
	// import Persp from './cameras/Persp.svelte';

	// geometry
	import Cube from '$lib/components/Canvas/utils/Cube.svelte';
	import TreeSquare from '$lib/components/Canvas/models/TreeSquare.svelte';
	import BushSquare from '$lib/components/Canvas/models/BushSquare.svelte';
	import House from './models/House.svelte';
	import Salesman from './models/Salesman.svelte';
	import Street from './models/Street.svelte';
	import Car from './models/Car.svelte';

	// lighting
	import Lights from '$lib/components/Canvas/lighting/Lights.svelte';

	// utilities
	// import Helpers from '$lib/components/Travel/utils/Helpers.svelte';
	import Background from '$lib/components/Canvas/utils/Background.svelte';
	import ShadowPlane from './utils/ShadowPlane.svelte';

	// tweened stores
	import { positionSalesman } from '$lib/stores/store';
	import { positionCar } from '$lib/stores/store';

	onMount(() => {
		positionCar.set(-50);
	});
</script>

<div>
	<Canvas rendererParameters={{ antialias: true }}>
		<!-- cameras -->
		<Ortho />
		<!-- <Persp /> -->

		<!-- lighting -->
		<Lights />

		<T.Group scale={0.1}>
			<!-- geometry -->
			<Cube />
			<House position={{ x: -20, y: 0, z: -6 }} />
			<House position={{ x: -8, y: 0, z: -6 }} />
			<House position={{ x: 8, y: 0, z: -6 }} />
			<House position={{ x: 16, y: 0, z: -6 }} />
			<House position={{ x: 32, y: 0, z: -6 }} />
			<T.Group position.x={$positionSalesman}>
				<Salesman />
			</T.Group>

			<T.Group position.x={$positionCar}>
				<Car />
			</T.Group>

			<TreeSquare variant="l1" position={{ x: 2, y: 0, z: -7 }} />
			<TreeSquare variant="s1" position={{ x: -15, y: 0, z: -10 }} />
			<TreeSquare variant="s1" position={{ x: -4, y: 0, z: -4 }} />
			<TreeSquare variant="s2" position={{ x: 12, y: 0, z: -9 }} />
			<TreeSquare variant="l1" position={{ x: 27, y: 0, z: -8 }} />
			<TreeSquare variant="s2" position={{ x: 24, y: 0, z: -5 }} />

			<BushSquare variant="l1" position={{ x: 4, y: 0, z: 7 }} />
			<BushSquare variant="l1" position={{ x: -17, y: 0, z: -4 }} />
			<BushSquare variant="s1" position={{ x: 6, y: 0, z: -4 }} />
			<BushSquare variant="s1" position={{ x: -7, y: 0, z: -4 }} />
			<BushSquare variant="s2" position={{ x: 8, y: 0, z: -4 }} />

			<Street />
		</T.Group>

		<!-- utilities -->
		<!-- <Helpers /> -->
		<Background color={'#739368'} />
		<ShadowPlane />
	</Canvas>
</div>

<style>
	div {
		height: 100%;
		width: 100%;
		min-height: 90vh;
	}
</style>
