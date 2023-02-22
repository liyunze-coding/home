<script lang="ts">
	import { onMount } from "svelte";

	let currentLocation = "Malaysia";

	let temperature_display: string;
	let weather_display: string;
	let location_display: string;
	let description_display: string;
	let humidity_display: string;
	let display_icon: string;
	let wind_display: string;

	let isCollapsed = true;

	function weatherSearch(event: any) {
		currentLocation = event.target[0].value;
		displayWeather();
	}

	function toggleCollapse() {
		isCollapsed = !isCollapsed;
	}

	function displayWeather() {
		fetch(
			`https://api.openweathermap.org/data/2.5/weather?q=${currentLocation}&units=metric&appid=0bf3216b6b5d548dd7bd5af83800ef23`
		)
			.then((response) => response.json())
			.then((data) => {
				const { name } = data;
				const { main, description, icon } = data.weather[0];
				const { temp, humidity } = data.main;
				const { speed } = data.wind;

				location_display = name;
				weather_display = main;
				temperature_display = `${Math.round(temp)}°C`;
				humidity_display = `${humidity}%`;
				description_display = description;
				display_icon = `https://openweathermap.org/img/wn/${icon}@2x.png`;
				wind_display = `${speed} km/h`;
			});
		currentLocation = "";
	}

	onMount(() => {
		displayWeather();
	});
</script>

<main>
	<div id="div-header" on:click={toggleCollapse} on:keydown>
		<h1>Weather</h1>
		<button id="collapse">
			{#if isCollapsed}
				<span>+</span>
			{:else}
				<span>-</span>
			{/if}
		</button>
	</div>

	<div
		style="visibility: {isCollapsed ? 'hidden' : 'visible'}"
		id="collapse-div"
	>
		<br />
		<p id="weather-header">
			{location_display} <span id="temp">{temperature_display}</span>
		</p>

		<br />

		<div id="weather-display">
			<img src={display_icon} alt="{weather_display} icon" />
			<div>
				<span style="font-weight:700">{weather_display}</span>
				<br />
				<span style="font-weight:300">{description_display}</span>
			</div>
		</div>
		<p id="weather-info">
			humidity: {humidity_display} <br />
			wind speed: {wind_display}
		</p>
		<form id="weather-search" on:submit|preventDefault={weatherSearch}>
			<input
				type="text"
				placeholder="Enter country/state"
				bind:value={currentLocation}
			/>
			<button type="submit">Search</button>
		</form>
	</div>
</main>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap");
	* {
		margin: 0;
		padding: 0;
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

	#div-header {
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

	#div-header:hover > #collapse {
		background-color: #f1f1f1;
		color: #141414;
	}

	#collapse-div {
		position: absolute;
		visibility: hidden;
		opacity: 0;
		transition: visibility 0s, opacity 0.5s linear;
	}

	#collapse-div[style*="visible"] {
		position: static;
		visibility: visible;
		opacity: 1;
	}

	#weather-display {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	#weather-header {
		font-weight: 500;
		font-size: 1.5em;

		display: flex;
	}

	#temp {
		font-weight: 300;
		font-size: 1.5em;
		margin-left: auto;
		margin-right: auto;
	}

	#weather-info {
		font-weight: bold;
		font-size: 0.8em;
	}

	#weather-search {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;

		margin-top: 10px;

		font-family: "Roboto", sans-serif;
	}

	#weather-search input[type="text"] {
		border: solid 2px #e1e1e1;
		border-radius: 5px;
		padding: 5px 10px;
		outline: none;
		font-size: 0.8em;

		width: 60%;
	}

	#weather-search input[type="text"]:focus {
		border: solid 2px #f1f1f1;
	}

	#weather-search button[type="submit"] {
		border: none;
		background-color: #141414;
		color: #f1f1f1;
		padding: 5px 10px;

		border: solid 2px white;
		border-radius: 5px;
		cursor: pointer;

		font-size: 0.8em;

		width: 30%;

		transition: background-color 400ms ease, color 400ms ease;
	}

	#weather-search button[type="submit"]:hover {
		background-color: #f1f1f1;
		color: #141414;
	}
</style>
