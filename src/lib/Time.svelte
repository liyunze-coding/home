<script lang="ts">
	let date: Date;
	let hour: number;
	let minute: number;
	let minute_display: string;
	let hour_display: string;
	let am_pm_display: string;
	let greeting: string = "morning";
	let visible: boolean = true;

	(function () {
		function addZero(i: number) {
			if (i < 10) {
				return `0${i}`;
			}
			return i.toString();
		}

		function formatTime(current_hour: number, current_minute: number) {
			let am_or_pm: string = hour < 12 ? "am" : "pm";
			if (current_hour === 0) {
				am_or_pm = "am";
			} else if (hour > 12) {
				current_hour -= 12;
			}

			return [
				addZero(current_hour),
				addZero(current_minute),
				am_or_pm,
			];
		}

		function updateTime() {
			date = new Date();
			hour = date.getHours();
			minute = date.getMinutes();
			let time_display = formatTime(hour, minute);

			hour_display = time_display[0];
			minute_display = time_display[1];
			am_pm_display = time_display[2];

			hour = date.getHours();
			if (hour < 12) {
				greeting = "morning";
			} else if (hour >= 12 && hour < 18) {
				greeting = "afternoon";
			} else {
				greeting = "evening";
			}

			setTimeout(updateTime, 1000);
		}
		updateTime();
	})();

	(function blink() {
		let blinking_elements =
			document.querySelectorAll<HTMLElement>(".blink");
		if (visible) {
			blinking_elements.forEach((el) => (el.style.opacity = "1"));
		} else {
			blinking_elements.forEach((el) => (el.style.opacity = "0"));
		}

		visible = !visible;

		setTimeout(blink, 1000);
	})();
</script>

<main>
	<h1>
		{hour_display}<span class="blink">:</span>{minute_display}
		{am_pm_display}
	</h1>
	<h2>
		Good {greeting}
	</h2>
	<p>hope you're feeling well ♡</p>
</main>

<style>
	h1,
	h2,
	p {
		font-family: "Courier New", Courier, monospace;
		text-align: center;
	}

	h1 {
		font-size: 3em;
	}

	h2 {
		font-size: 2em;
	}

	p {
		font-size: 1.2em;
	}

	main {
		margin: 0;
		padding: 0;
	}
</style>
