<script>
    //todo: add animation when clicked
    import { getContext } from "svelte";
    let { theme } = getContext("theme");

    $: settingsImage =
        $theme == "light"
            ? "./assets/icons8-settings.svg"
            : "./assets/icons8-settings-light.svg";
    $: closeSettingsImage =
        $theme == "light"
            ? "./assets/icons8-close.svg"
            : "./assets/icons8-close-light.svg";

    export let settingsVisible = false;
</script>

<button
    on:click|preventDefault={() => {
        settingsVisible = !settingsVisible;
    }}
>
    {#if settingsVisible}
        <img src={closeSettingsImage} alt="Close settings" />
    {:else}
        <img src={settingsImage} alt="Open settings" />
    {/if}
</button>

<style>
    button {
        background-color: transparent;

        width: 30px;
        height: 30px;

        border: 0;
        padding: 0;
        margin: 0;
    }
    button:active {
        background-color: transparent;
    }
    img {
        width: 100%;
        height: auto;
    }
</style>
