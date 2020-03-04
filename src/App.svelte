<Tailwindcss />

<div class="w-full h-full flex items-center justify-center bg-gray-200">
	<div>
		<div class="pb-2 text-gray-500 text-sm">Wykonano: <strong>{numberOfCompletedTodos}</strong> zadań</div>

		<form class="flex pb-4" on:submit|preventDefault={addNewTodo}>
			<input bind:value={newTodoName} type="text" class="px-3 py-2 rounded" placeholder="Wpisz nazwę zadania">
			<button class="px-3 py-2 ml-2 bg-blue-500 text-white font-bold uppercase rounded">Dodaj</button>
		</form>

		
		{#each todos as todo}
			<label 
				class="block px-4 py-3 mb-2 flex items-center cursor-pointer rounded {todo.done ? 'bg-green-300 text-green-700' : 'bg-gray-300 text-gray-700'}" 
				transition:fade
				>
				<input type="checkbox" bind:checked={todo.done}>
				<div class="pl-3">
					{todo.name}
				</div>
			</label>
		{/each}
	</div>
</div>

<script>
	import { fade, fly } from 'svelte/transition';
	import Tailwindcss from './Tailwindcss.svelte';

	let todos = [];
	let newTodoName = '';

	$: numberOfCompletedTodos = todos.filter(e => e.done).length;

	function addNewTodo() {
		todos = todos.concat({ name: newTodoName, done: false });
		newTodoName = '';
	}
</script>