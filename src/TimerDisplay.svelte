<script>
    export let duration;
    $: minutes_text =
        Math.floor(duration / 60) % 60 < 10
            ? "0" + (Math.floor(duration / 60) % 60)
            : "" + (Math.floor(duration / 60) % 60);
    $: seconds_text =
        duration % 60 < 10 ? "0" + (duration % 60) : "" + (duration % 60);
</script>

<p>
    {minutes_text}:{seconds_text}
</p>

<style>
    p {
        font-size: 72px;
        margin: 0;
    }
</style>
