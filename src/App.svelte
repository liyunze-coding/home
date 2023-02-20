<script lang="ts">
	import Time from "./lib/Time.svelte";
	import Reminders from "./lib/Reminders.svelte";
	import Quote from "./lib/Quote.svelte";
	import Weather from "./lib/Weather.svelte";
</script>

<main>
	<div id="time"><Time /></div>
	<div id="reminders"><Reminders /></div>
	<div id="quote"><Quote /></div>
	<div id="weather"><Weather /></div>
</main>

<style>
	main {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;

		height: 100vh;
	}

	#reminders {
		position: absolute;
		top: 2%;
		right: 2%;
	}

	#quote {
		position: absolute;
		bottom: 5%;
		left: 50%;
		transform: translateX(-50%);
		text-align: center;
	}

	#weather {
		position: absolute;
		top: 50%;
		left: 2%;

		transform: translateY(-50%);
	}
</style>
