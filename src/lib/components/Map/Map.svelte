<script lang="ts">
	import River from '../River/River.svelte';
	import { subwayLines } from './mocks';
	import type { iSubwayStation } from '../../interfaces';
	import { curveCatmullRom, line } from 'd3';
	import type { Line } from 'd3';

	const lineGenerator: Line<[number, number]> = line().curve(curveCatmullRom.alpha(1));

	// filter through all nodes and get only those that have a name -> hence a station
	// TODO: consider having styling nodes and stations separately
	const getSwStations = (nodes: iSubwayStation[]) => nodes.filter(({ name }) => !!name);
</script>

<template>
	<River />

	<svg id="map" height="747" width="100%" viewBox="0 0 3500 3500" fill="none">
		{#each subwayLines as { nodes, colorCode, name } (name)}
			<g fill="none">
				<path
					d={lineGenerator(nodes.map(({ point }) => Object.values(point)))}
					stroke={colorCode}
					stroke-width="30"
				/>

				{#each getSwStations(nodes) as { name, point: { x, y } } (name)}
					<circle cx={x} cy={y} fill={colorCode} r="50" />
					<text>{name}</text>
				{/each}
			</g>
		{/each}
	</svg>
</template>

<style>
	#map {
		z-index: 1;
	}
</style>
