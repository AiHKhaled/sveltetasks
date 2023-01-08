<script lang="ts">
	import Header from '../components/Header.svelte';
	import TodoList from '../components/TodoList.svelte';
	import Form from '../components/Form.svelte';

	let todos = [
		{ id: 1, text: 'First', completed: false },
		{ id: 2, text: 'Second', completed: true },
		{ id: 3, text: 'Third', completed: true }
	];
	let completedTodos: number;
	let remainedTodos: number;
	let newTodo: string;

	$: completedTodos = todos.length;
	$: remainedTodos = todos.reduce((n, todo) => {
		return n + (todo.completed ? 0 : 1);
	}, 0);

	const onComplete = (e: any) => {
		let updatedId = e.detail.id;

		todos.map((todo) => {
			if (todo.id == updatedId) todo.completed = !todo.completed;
		});
		todos = todos;
	};
	const addTodo = () => {
		newTodo = newTodo;
		if (newTodo.trim() != '') {
			let newID = Math.max(...todos.map((todo) => todo.id)) + 1;
			todos = [...todos, { id: newID, text: newTodo, completed: false }];
		}
		newTodo = '';
	};

	const deleted = (e: any) => {
		let delID = e.detail.id;
		todos = todos.filter((todo) => {
			return todo.id != delID;
		});
	};
</script>

<div id="app-container" class="app-container">
	<Header {remainedTodos} {completedTodos} />

	<TodoList {todos} on:completed={onComplete} on:deleted={deleted} />

	<Form bind:newTodo on:created={addTodo} />
</div>

<style>
	.app-container {
		width: 400px;
		min-height: 500px;
		background-color: #282c34;
		box-shadow: 0 20px 80px rgba(0, 0, 0, 0.6);
		background: radial-gradient(circle, #282c34 0%, rgba(40, 48, 56, 1) 100%);
		position: relative;
		border-radius: 1em;
		padding: 20px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}
</style>
