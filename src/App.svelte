<script>
	import { ThemeWrapper, ThemeToggle } from "svelte-themer";
	import themes from "./themes.js";

	import PomoTimer from "./PomoTimer.svelte";
</script>

<ThemeWrapper {themes}>
	<main>
		<!-- <ThemeToggle /> -->
		<PomoTimer />
	</main>
</ThemeWrapper>

<style>
	:global(html) {
		background-color: var(--theme-colors-background, initial);
	}

	main {
		max-width: 480px;
		margin: 0 auto;
	}

	/* @media (min-width: 640px) {
		main {
			max-width: none;
		}
	} */
</style>
