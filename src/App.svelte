<form class="flex" on:submit|preventDefault={addNewTodo}>
	<input type="text" bind:value={newTodoName}>
	<button>Dodaj nowe zadanie</button>
</form>

<div>
	Wykonano: <strong>{numberOfCompletedTodos}</strong> zadań
</div>

{#each todos as todo}
	<div>
		<label>
			<input type="checkbox" bind:checked={todo.done}>
			{todo.name}
		</label>
	</div>
{/each}

<script>
	let todos = [];
	let newTodoName = '';

	$: numberOfCompletedTodos = todos.filter(e => e.done).length;

	function addNewTodo() {
		todos = todos.concat({ name: newTodoName, done: false });
		newTodoName = '';
	}
</script>