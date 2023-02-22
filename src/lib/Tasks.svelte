<script lang="ts">
	import { onMount } from "svelte";

	let isCollapsed = true;

	function toggleCollapse() {
		isCollapsed = !isCollapsed;
	}

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
	<div id="header" on:click={toggleCollapse} on:keydown={toggleCollapse}>
		<h1>Tasks</h1>
		<button id="collapse">
			{#if isCollapsed}
				<span>+</span>
			{:else}
				<span>-</span>
			{/if}
		</button>
	</div>
	<div
		id="tasks-body"
		style="visibility: {isCollapsed ? 'hidden' : 'visible'}"
	>
		<br />
		<form on:submit|preventDefault={handleOnSubmit}>
			<input
				id="input-field"
				type="text"
				value={task}
				autocomplete="off"
			/>
			<button id="submit-button" type="submit">Add task</button>
		</form>

		<ul id="task-boxes">
			{#each tasks as task}
				<li
					class="task"
					on:click={removeTask}
					on:keydown={removeTask}
				>
					{task}
				</li>
			{/each}
		</ul>
	</div>
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

	main {
		font-family: "Roboto", sans-serif;
		display: block;

		border: solid 2px white;
		border-radius: 20px;

		padding: 20px;

		background-color: #242424;

		width: clamp(250px, 20%, 400px);
	}

	#header {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;

		font-size: 70%;

		cursor: pointer;

		/* width: 250px; */
	}

	#collapse {
		margin-left: 10px;

		font-size: 1.5em;
		padding: 0 8px 2px 8px;

		font-family: monospace;

		border: solid 2px #f1f1f1;
		color: #f1f1f1;

		background: #141414;

		transition: all 400ms ease;

		/* transform: translateY(-3px); */
	}

	#header:hover > #collapse {
		background-color: #f1f1f1;
		color: #141414;
	}

	#tasks-body {
		position: absolute;
		visibility: hidden;
		opacity: 0;

		transition: visibility 0s, opacity 0.5s linear;
	}

	#tasks-body[style*="visible"] {
		position: static;
		visibility: visible;
		opacity: 1;
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
		/* border-bottom: solid 2px #242424; */
		margin-top: 5px;
		margin-left: 5%;

		text-align: left;

		transition: 0.2s border;

		cursor: pointer;
	}

	.task:hover {
		text-decoration: line-through #fafafa solid 2px;
	}
</style>
