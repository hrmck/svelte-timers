<script>
    import { getContext } from "svelte";
    let { toggle, theme } = getContext("theme");

    const themeImage = (theme) => {
        switch (theme) {
            case "light":
                return "./assets/icons8-moon-symbol.png";
            case "dark":
                return "./assets/icons8-iron-man.svg";
            default:
                return "./assets/icons8-sun.svg";
        }
    };

    $: currentImage = themeImage($theme);
</script>

<button on:click={toggle}>
    <img src={currentImage} alt="Toggle theme" />
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
