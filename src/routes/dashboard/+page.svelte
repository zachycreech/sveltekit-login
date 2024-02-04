<script lang="ts">
	let todoList: string[] = ['First', 'Second', 'Third'];
	let todoText = '';

	function handleAdd() {
		todoList = [...todoList, todoText];
		todoText = '';
	}

	function handleSubmit() {
		console.log(todoList);
	}

	function handleEdit(index: number) {
		let newToDoList = [...todoList].filter((_, i) => i !== index);
		todoText = newToDoList[index];
		todoList = newToDoList;
	}
	function handleDelete(item: string) {
		let newToDoList = [...todoList].filter((i) => i !== item);
		todoList = newToDoList;
	}
</script>

<div class="mainContainer">
	<div class="toDoHeader">
		<h1>To-Do's</h1>
		<button on:click={handleSubmit}>
			<div class="save">
				<i class="fa-solid fa-floppy-disk"></i>
				<p>Save</p>
			</div>
		</button>
		<button>
			<div class="save">
				<p>Log Out</p>
				<i class="fa-solid fa-arrow-right-from-bracket"></i>
			</div>
		</button>
	</div>
	<main>
		{#each todoList as item, i}
			<div class="todoList">
				<p>{i + 1}. {item}</p>
				<div class="options">
					<button on:click={() => handleEdit(i)}>
						<i class="fa-solid fa-pencil"></i>
					</button>
					<button on:click={() => handleDelete(item)}>
						<i class="fa-solid fa-trash"></i>
					</button>
				</div>
			</div>
		{/each}
	</main>
	<form>
		<div class="todoGroup">
			<input type="text" bind:value={todoText} placeholder="Add a to-do" />
			<button on:click={handleAdd}>Add</button>
		</div>
	</form>
</div>

<style>
	.mainContainer {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
		gap: 24px;
		padding: 24px;
		width: 100%;
		max-width: 1000px;
		margin: 0 auto;
	}

	.toDoHeader {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	form {
		display: flex;
		justify-content: center;
		align-items: stretch;
		gap: 0.5rem;
	}
	main {
		flex: 1;
	}

	.todoGroup {
		display: flex;
		justify-content: center;
		align-items: stretch;
		gap: 0.5rem;
		width: 100%;
	}
	.todoGroup input {
		width: 100%;
		border: none;
		color: white;
		background: transparent;
		outline: none;
		padding: 0.7rem;
		display: flex;
		border: 1px solid gray;
		overflow: hidden;
	}
	button {
		background: purple;
		color: white;
		border: none;
		padding: 0.7rem;
		border-radius: 0.1rem;
		cursor: pointer;
	}
	button:hover {
		background: rebeccapurple;
	}
	.save {
		display: flex;
		align-items: center;
		gap: 0.5rem;
	}
	.options {
		display: flex;
		gap: 0.8rem;
	}
	.options i {
		cursor: pointer;
		padding: 0.5rem;
		font-size: 1.2rem;
	}
	.options i:hover {
		color: purple;
	}
	.todoList {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		gap: 0.5rem;
	}
	.todoList button {
		background: transparent;
		border: none;
		cursor: pointer;
		margin: 0;
		padding: 0;
	}
</style>
