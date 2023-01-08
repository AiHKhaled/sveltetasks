<script lang="ts">
	export let completedTodos: number;
	export let remainedTodos: number;
</script>

<div class="app-header">
	<div>{completedTodos} Total</div>
	<div class="task-count">{remainedTodos} Remaining</div>
</div>

<style>
	.app-header {
		padding: 10px;
		display: flex;
		justify-content: space-between;
	}

	.task-count {
		align-self: center;
	}
</style>
