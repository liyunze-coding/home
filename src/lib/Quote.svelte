<script lang="ts">
	import { onMount } from "svelte";

	function readTextFile(file: string) {
		var rawFile = new XMLHttpRequest();
		rawFile.open("GET", file, false);
		rawFile.onreadystatechange = function () {
			if (rawFile.readyState === 4) {
				if (rawFile.status === 200 || rawFile.status == 0) {
					let allText = rawFile.responseText;

					let quotes = allText.split("\n");

					let quote =
						quotes[Math.floor(Math.random() * quotes.length)];

					document.getElementById(
						"quote"
					).innerText = `${quote}`;
				}
			}
		};

		rawFile.send(null);
	}

	onMount(() => {
		readTextFile("./src/assets/quotes.txt");
	});
</script>

<p id="quote" />

<style>
	#quote {
		font-size: 15px;

		color: #fafafa;
	}
</style>
