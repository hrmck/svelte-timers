<script>
    export let timers;
    export let currentTimer;
    export let timerStarted;
</script>

<div>
    {#each timers as timer}
        <button
            class="timer__{currentTimer == timer ? 'active' : ''}"
            disabled={timerStarted}
            on:click={() => {
                currentTimer = timer;
            }}
        >
            {timer.label}
        </button>
    {/each}
</div>

<style>
    div {
        display: flex;
        flex-flow: row nowrap;
    }

    button {
        flex-grow: 1;

        background-color: transparent;
        color: inherit;
        font-size: 24px;

        border: 3px solid;
        border-radius: 0;
        padding: 12px;
        margin: -1px;
    }
    button:first-of-type {
        border-radius: 10px 0 0 10px;
    }
    button:last-of-type {
        border-radius: 0 10px 10px 0;
    }
    button:hover {
        background-color: var(--theme-colors-primary_dark);
    }

    .timer__active {
        background-color: var(--theme-colors-secondary);
    }
</style>
