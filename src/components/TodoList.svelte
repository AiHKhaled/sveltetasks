<script lang="ts">
	import Todo from './Todo.svelte';
	type Todo = {
		id: number;
		text: string;
		completed: boolean;
	}[];
	export let todos: Todo;
</script>

<div class="app-body">
	<ul>
		{#each todos as todo}
			<Todo key={todo.id} itemText={todo.text} completed={todo.completed} on:completed on:deleted />
		{/each}
	</ul>
</div>

<style>
	ul {
		border-top: 1px solid rgb(121, 121, 121);
		padding-top: 10px;
		list-style-type: none;
		padding-left: 0px;
	}

	.app-body {
		flex-grow: 1;
		max-height: 600px;
		overflow-x: hidden;
	}
</style>
