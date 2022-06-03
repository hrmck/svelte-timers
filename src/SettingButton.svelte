<script>
    //todo: add animation when clicked
    let settingsImage = "./assets/settings.png";
    let closeSettingsImage = "./assets/close.png";
    export let settingsVisible = false;
</script>

<button
    on:click|preventDefault={() => {
        settingsVisible = !settingsVisible;
    }}
    id="image-button"
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

        border: 0;
        padding: 0;
        margin: 0;
    }
</style>
