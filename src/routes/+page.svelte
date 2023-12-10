<script lang="ts">
	import mermaid from 'mermaid';
	import { onMount } from 'svelte';

	const kph = 34;
	let diagram = `\
  
    gantt
    tickInterval 1hour
    title Truxport Line 1
    axisFormat %
    Section RUSH
    
    section TT A
        
    section TT B
        B 01 - 06  :b01, after g01, ${64 / kph}h
        B 07 - 34  :b02, after h01, ${334 / kph}h
    section TT C
        
    section TT D
        D 07 - 34 :d1, 2023-12-10, ${328 / kph}h
    section TT E
        E 01 - 02 :e01, after d1, ${24 / kph}h
    section TT F
        F 01      :f01, after e01, ${1 / kph}h
    section TT G
        G 18 - 35 :g01, after x01, ${210 / kph}h
    section TT H
        H 01 - 34 :h01, after g01, ${408 / kph}h
    section TT X
        X 01 - 02 :x01, after f01, ${36 / kph}h
    `;

	let container: HTMLElement;

	async function renderDiagram() {
		// console.log(diagram);
		const { svg } = await mermaid.render('mermaid', diagram);
		container.innerHTML = svg;
	}

	onMount(() => {
		renderDiagram();
	});
</script>

<main>
	<div>
		<p>A demo of how a TT Gantt chart might look.</p>
		<p>Kits per hour: {kph}</p>
	</div>
	<!-- <pre contenteditable="true" bind:innerHTML={diagram}></pre> -->
	<span bind:this={container}></span>
</main>

<style global>
	.grid .tick {
		stroke: lightgrey !important;
		opacity: 0.3 !important;
		shape-rendering: crispEdges !important;
	}

	.today {
		opacity: 0 !important;
	}
</style>
