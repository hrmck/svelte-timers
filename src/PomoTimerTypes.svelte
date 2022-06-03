<script>
    export let timers;
    export let currentTimer;
    export let timerStarted;
</script>

<div>
    {#each timers as timer}
        <button
            on:click={() => {
                currentTimer = timer;
            }}
            class="timer__{currentTimer == timer ? 'active' : ''}"
            disabled={timerStarted}
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

        font-size: 24px;
        border-radius: 0;
    }
    button:first-of-type {
        border-radius: 10px 0 0 10px;
    }
    button:last-of-type {
        border-radius: 0 10px 10px 0;
    }
    button:focus {
        background-color: transparent;
    }

    .timer__active {
        background-color: var(--theme-colors-secondary) !important;
        border-color: var(--theme-colors-text) !important;
    }
</style>
