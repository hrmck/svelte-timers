<script>
	import { ThemeWrapper } from "svelte-themer";
	import themes from "./themes.js";

	import PomoTimer from "./PomoTimer.svelte";
</script>

<ThemeWrapper {themes}>
	<main>
		<PomoTimer />
	</main>
</ThemeWrapper>

<style>
	:global(html) {
		background-color: var(--theme-colors-background-contrast, initial);
	}

	:global(button) {
		background-color: var(--theme-colors-primary_dark);
		color: inherit;

		border: 2px solid;
		border-radius: 10px;
		padding: 12px;
		margin: 0;
	}
	:global(button:hover) {
		background-color: var(--theme-colors-primary);
		color: var(--theme-colors-text-accent);
	}

	main {
		max-width: 480px;
		margin: 0 auto;
	}
</style>
