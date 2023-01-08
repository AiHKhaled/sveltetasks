<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { fly } from 'svelte/transition';
	export let itemText: string;
	export let completed: boolean;
	export let key: number;

	const dispatch = createEventDispatcher();
	const completedTodo = (id: number) => {
		dispatch('completed', { id: id });
	};
	const deleteTodo = (id: number) => {
		dispatch('deleted', { id: id });
	};
</script>

<li
	transition:fly={{ y: 200, duration: 1000 }}
	class="todo-list list-item-view {completed ? 'completed' : ''}"
>
	<span>
		<button
			on:click={() => completedTodo(key)}
			class="btn btn-done fa-solid {completed ? 'fa-square-check' : 'fa-square'}"
		/>
		<span>{itemText}</span>
	</span>
	<button class="btn btn-delete fa-solid fa-trash" on:click={() => deleteTodo(key)} />
</li>

<style>
	.btn {
		color: inherit;
		cursor: pointer;
		font-size: 15px;
		padding: 10px 12px;
		border-radius: 2em;
		background: none;
		border: 0px solid;
		transition: 250ms ease-out;
	}

	.btn:hover {
		background: #1d2025;
	}

	.btn:focus {
		outline: none;
	}

	.list-item-view {
		padding-top: 5px;
		padding-bottom: 0px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.completed {
		color: #6a6f75;
		opacity: 0.5;
	}
</style>
