<script>
	let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
	let newTask = "";
	function saveTasks() {
		localStorage.setItem('tasks', JSON.stringify(tasks));
	}
	function addTask() {
		if (newTask.trim() !== "") {
			tasks = [
				...tasks,
				{ id: tasks.length + 1, text: newTask, completed: false },
			];
			newTask = "";
			saveTasks();
		}
	}

	function removeTask(id) {
		tasks = tasks.filter((task) => task.id !== id);
		saveTasks();
	}

	function toggleTask(id) {
		tasks = tasks.map((task) =>
			task.id === id ? { ...task, completed: !task.completed } : task,
		);
		saveTasks();
	}
</script>

<main>
	<div class="container">
		<div class="todo-app">
			<h2>Gk's To-Do List<img src="images/icon.png" alt="" /></h2>
			<div class="row">
				<input bind:value={newTask} placeholder="Add a text" />
				<button class="btn" on:click={addTask}>Add</button>
			</div>
			<ul>
				{#each tasks as { id, text, completed }}
					<li key={id} class:completed>
						<div class="list_data">
							<div class="list">
								<img
									class="img"
									on:click={() => toggleTask(id)}
									src={completed
										? "images/checked.png"
										: "images/unchecked.png"}
									alt={completed ? "Checked" : "Unchecked"}
								/>
								<span class={completed ? "checked-text" : ""}
									>{text}</span
								>
							</div>

							<div>
								
								<button
									class="btn2"
									on:click={() => removeTask(id)}
								>
									x
								</button>
							</div>
						</div>
					</li>
				{/each}
			</ul>
		</div>
	</div>
</main>

<style>
	/* main {
	  text-align: center;
	  max-width: 240px;
	  margin: 0 auto;
	  padding: 20px;
	} */
	.btn {
		border: none;
		outline: none;
		padding: 16px 50px;
		background: #ff5945;
		color: #fff;
		font-size: 16px;
		cursor: pointer;
		/* border-radius: 40px; */
		height: 6vh;
		margin: 0;
	}
	.btn2 {
		color: #ff5945;
		border: none;
	}
	.btn1 {
		border: none;
		outline: none;
		padding: 12px 28px;
		background: #ff5945;
		color: #fff;
		font-size: 16px;
		cursor: pointer;
		border-radius: 40px;
	}
	.list_data {
		display: flex;
		width: 100%;
		align-items: center;
		justify-content: space-between;
	}
	.list {
		display: flex;
		align-items: center;
		width: 50%;
		gap: 20px;
	}

	.container {
		width: 100%;
		min-height: 100vh;
		background: linear-gradient(135deg, #153677, #4e085f);
		padding: 10px;
	}
	.row {
		display: flex;
		align-items: center;
		justify-content: space-between;
		background: #edeef0;
		/* border-radius: 30px; */
		padding-left: 20px;
		margin-bottom: 25 px;
	}

	input {
		flex: 1;
		border: none;
		outline: none;
		background: transparent;
		padding: 10px;
		font-weight: 14px;
		height: 6vh;
		margin: 0;
	}

	.todo-app {
		width: 100%;
		max-width: 540px;
		background: #fff;
		margin: 100px auto 20px;
		padding: 40px 30px 70px;
		border-radius: 10px;
	}
	.todo-app h2 {
		color: #002765;
		display: flex;
		align-items: center;
		margin-bottom: 20px;
	}

	.todo-app h2 img {
		width: 30px;
		margin-left: 10px;
	}

	ul {
		list-style: none;
		padding: 0;
	}

	li {
		display: flex;
		justify-content: space-between;
		padding: 8px;
		background-color: #e7e7e729;
		margin-bottom: 5px;
		border-radius: 31px;
	}

	.img {
		width: 32px;
		height: 3vh;
	}

	li.completed {
		text-decoration: line-through;
	}
	/* .checked-text {
		text-decoration: line-through;
	} */
</style>
