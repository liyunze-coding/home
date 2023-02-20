<script lang="ts">
	let temperature_display: string;
	let weather_display: string;
	let location_display: string;
	let description_display: string;
	let humidity_display: string;
	let display_icon: string;
	let wind_display: string;

	fetch(
		"https://api.openweathermap.org/data/2.5/weather?q=Kuala+Lumpur&units=metric&appid=0bf3216b6b5d548dd7bd5af83800ef23"
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
</script>

<div id="weather-div">
	<h2>{location_display}</h2>
	<br />
	<span id="temp">{temperature_display}</span>
	<div id="weather-display">
		<img src={display_icon} alt="{weather_display} icon" />
		<div>
			<span style="font-weight:700">{weather_display}</span> <br />
			<span style="font-weight:300">{description_display}</span>
		</div>
	</div>
	<p id="weather-info">
		humidity: {humidity_display} <br />
		wind speed: {wind_display}
	</p>
</div>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap");
	* {
		margin: 0;
		padding: 0;
	}

	#weather-div {
		font-family: "Roboto", sans-serif;
		display: block;

		border: solid 2px white;
		border-radius: 20px;

		padding: 20px;
		width: 250px;
	}
	#weather-display {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	#temp {
		font-weight: 300;
		font-size: 2em;
	}

	#weather-info {
		font-weight: 300;
		font-size: 1em;
	}
</style>
