<script lang="ts">
	import Time from "./lib/Time.svelte";
	import Tasks from "./lib/Tasks.svelte";
	import Quote from "./lib/Quote.svelte";
	import Weather from "./lib/Weather.svelte";
</script>

<main>
	<div id="tools">
		<div id="weather"><Weather /></div>
		<div id="tasks-component"><Tasks /></div>
	</div>
	<div id="time"><Time /></div>
	<div id="quote-div"><Quote /></div>
</main>

<style>
	main {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;

		height: 100vh;
		width: 100vw;
	}

	#quote-div {
		position: absolute;
		bottom: 5%;
		left: 50%;
		transform: translateX(-50%);
		text-align: center;
		width: clamp(300px, 50vw, 500px);
	}

	#tools {
		/* width: 100vw; */
		width: fit-content;
		/* height: 100vh; */

		position: absolute;
		top: 1%;
		left: 0;

		display: flex;
		flex-direction: column;
		/* align-items: center; */
		justify-content: space-between;
	}

	#tools div {
		width: fit-content;
	}

	#tools div:not(:last-child) {
		margin-bottom: 10px;
	}

	@media (max-width: 600px) {
		#tools {
			display: flex;
			/* flex-direction: column; */
		}

		#tools div {
			position: static;

			width: 40%;
		}
	}
</style>
