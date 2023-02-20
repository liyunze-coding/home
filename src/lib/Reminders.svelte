<script lang="ts">
	import { onMount } from "svelte";

	function remove(arr: Array<string>, value: string) {
		var index = arr.indexOf(value);
		if (index > -1) {
			arr.splice(index, 1);
		}
		return arr;
	}
	let tasks = [];
	let task = "";

	// onMount(() => {
	// 	const existingReminders = localStorage.getItem("reminders");
	// 	tasks = JSON.parse(existingReminders) || [];
	// });

	const handleOnSubmit = (e: any) => {
		task = e.target[0].value.trim();

		if (!tasks.includes(task) && task !== "") {
			tasks = [...tasks, task];
			// localStorage.setItem("reminders", JSON.stringify(tasks));
		}

		task = "";
	};

	const removeTask = (e: any) => {
		let removed_task = e.target.innerText;
		tasks = [...remove(tasks, removed_task)];
		// localStorage.setItem("reminders", JSON.stringify(tasks));
	};
</script>

<main>
	<form on:submit|preventDefault={handleOnSubmit}>
		<input id="input-field" type="text" value={task} autocomplete="off" />
		<button id="submit-button" type="submit">Add task</button>
	</form>

	<ul id="task-boxes">
		{#each tasks as task}
			<li class="task" on:click={removeTask} on:keydown={removeTask}>
				{task}
			</li>
		{/each}
	</ul>
</main>

<style>
	* {
		margin: 0;
		padding: 0;
	}

	form {
		display: flex;
		flex-direction: row;
	}

	#input-field {
		font-size: 15px;

		width: 150px;

		background-color: #242424;
		color: #f1f1f1;

		outline: 0;
		border: none;

		border-bottom: solid 2px #fafafa;
	}

	#submit-button {
		width: 100px;

		padding: 10px;
		margin-left: 10px;

		background-color: #181818;
		color: #f1f1f1;

		border: solid 2px #fafafa;
		border-radius: 5px;

		transition: background-color 0.5s;
	}

	#submit-button:hover {
		background-color: #fafafa;
		color: #181818;
	}

	#input-field:focus,
	#submit-button:focus {
		outline: 0;
	}

	#task-boxes {
		display: block;

		list-style-type: circle;
	}

	.task {
		width: fit-content;
		max-width: 250px;
		border-bottom: solid 2px #242424;
		margin-top: 5px;
		margin-left: 5%;

		text-align: left;

		transition: 0.2s border;

		cursor: pointer;
	}

	.task:hover {
		border-bottom: solid 2px white;
	}
</style>
