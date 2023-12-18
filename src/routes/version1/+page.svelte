<script lang="ts">
	interface OrderBaseProperties {
		line: 'TT' | 'LT' | 'LP' | 'IM' | 'HC';
		workOrderNumber: number;
		priorityNumber: number;
	}

	type WorkOrderOnList = OrderBaseProperties & {
		orderLetter: 'A' | 'B' | 'C' | 'D' | 'E' | 'F' | 'G' | 'H' | 'X';
	};
	type WorkOrderAsRush = OrderBaseProperties & {
		orderLetter: 'R';
	};

	interface List {
		listLetter: 'A' | 'B' | 'C' | 'D' | 'E' | 'F' | 'G' | 'H' | 'X';
		rush?: never;
		startOrder: number;
		endOrder: number;
		orders: WorkOrderOnList | WorkOrderOnList[];
	}

	interface Rush {
		listLetter?: never;
		rush: 'R';
		order: WorkOrderAsRush;
	}

	type OrderSegment = List | Rush;
</script>

<div id="add-to-list">
	<label for="priority">Priority</label>
	<input id="priority" type="text" />

	<label for="list-letter">List Letter</label>
	<input id="lsit-letter" type="text" />

	<label for="line">Line</label>
	<input id="line" type="text" />

	<div id="rush-checkbox">
		<label for="rush">Rush?</label>
		<input id="rush" type="checkbox" />
	</div>

	<input type="button" value="submit" />
</div>

<style>
	#add-to-list {
		width: 200px;
		display: flex;
		flex-direction: column;
		align-items: start;
	}

	#rush-checkbox {
		display: flex;
	}

	#rush-checkbox > input {
		padding-left: 5px;
	}
</style>
