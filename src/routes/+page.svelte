<script lang="ts">
	import mermaid from 'mermaid';
	import { onMount } from 'svelte';

	const kph = 34;
	let tt1diagram = `\
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
        D 07 - 34 :d01, 2023-12-10, ${328 / kph}h
    section TT E
        E 01 - 02 :e01, after d01, ${24 / kph}h
    section TT F
        F 01      :f01, after e01, ${1 / kph}h
    section TT G
        G 18 - 35 :g01, after x01, ${210 / kph}h
    section TT H
        H 01 - 34 :h01, after b01, ${408 / kph}h
    section TT X
        X 01 - 02 :x01, after f01, ${36 / kph}h
    `;

	let tt2diagram = `\
    gantt
    tickInterval 1hour
    title Truxport Line 2
    axisFormat %
    Section RUSH

    section TT A
        A 09 - 17, :a01, 2023-12-10, ${108 / kph}h
    section TT B
        
    section TT C
        C 01 - 17, :c01, after f01, ${204 / kph}h
    section TT D
        
    section TT E
        E 03 - 18, :e01, after a01, ${176 / kph}h
    section TT F
        F 02 - 18, :f01, after e01, ${200 / kph}h
    section TT G
        
    section TT H
        
    section TT X
        
    `;

	let tt1container: HTMLElement;
	let tt2container: HTMLElement;

	async function renderDiagram() {
		// console.log(diagram);
		const ttRender1 = await mermaid.render('mermaid', tt1diagram);
		const ttRender2 = await mermaid.render('mermaid', tt2diagram);
		tt1container.innerHTML = ttRender1.svg;
		tt2container.innerHTML = ttRender2.svg;
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
	<span bind:this={tt1container}></span>
	<span bind:this={tt2container}></span>
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
