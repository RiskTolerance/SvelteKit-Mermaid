<script lang="ts">
	import mermaid from 'mermaid';
	import { onMount } from 'svelte';

	const kph = 34;

	// Define the structure for your tasks
	interface Task {
		priority?: number;
		name: string;
		start: string;
		duration: string;
	}

	// Sample tasks data
	let tasks: Task[] = [
		{ name: 'Task A', start: '2023-12-10', duration: '5h' },
		{ name: 'Task B', start: '2023-12-10', duration: '5h' }
		// Add more tasks as needed
	];

	// Function to generate Gantt chart string
	function generateGanttString(tasks: Task[]): string {
		let chartString = `\
        gantt
        tickInterval 1hour
        title Truxport Line 1
        axisFormat %
        Section RUSH
        `;

		tasks.forEach((task) => {
			chartString += `section ${task.name}\n`;
			chartString += `    ${task.name} :${task.start}, ${task.duration}\n`;
		});

		return chartString;
	}

	let tt1container: HTMLElement;

	async function renderDiagram(diagramString: string) {
		const ttRender1 = await mermaid.render('mermaid', diagramString);
		tt1container.innerHTML = ttRender1.svg;
	}

	onMount(() => {
		const diagramString = generateGanttString(tasks);
		renderDiagram(diagramString);
	});

	// Function to update the chart when tasks change
	function updateChart() {
		const diagramString = generateGanttString(tasks);
		renderDiagram(diagramString);
	}

	// Call updateChart() whenever tasks change
</script>

<main>
	<div>
		<p>A demo of how a TT Gantt chart might look.</p>
		<p>Kits per hour: {kph}</p>
		<!-- Add form elements to update tasks here -->
	</div>
	<span bind:this={tt1container}></span>
</main>
