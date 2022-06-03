<script>
    export let workCount = 0;
    export let targetWorkCount = 4;
</script>

<div>
    {#each Array(workCount) as _, index (index)}
        <span class="tomato filled" />
    {/each}
    {#each Array(targetWorkCount - workCount) as _, index (index)}
        <span class="tomato" />
    {/each}
</div>

<style>
    div {
        display: flex;
        flex-flow: row wrap;
        justify-content: center;
    }
    .tomato {
        height: 24px;
        width: 24px;
        border: 2px solid var(--theme-colors-text);
        border-radius: 50%;
        margin: 3px 10px;
    }
    .filled {
        background-color: var(--theme-colors-text);
    }
</style>
