<script>
    import { createEventDispatcher } from "svelte";
    let dispatch = createEventDispatcher();

    export let workDuration = 25;
    export let shortRestDuration = 5;
    export let longRestDuration = 10;
    export let timerStarted = false;
    export let autoStartTimer = false;

    let workDurationInput;
    let shortRestDurationInput;
    let longRestDurationInput;

    const editTimerSettings = () => {
        dispatch("updateTimerSettings", {
            workDurationInput: workDurationInput * 60,
            shortRestDurationInput: shortRestDurationInput * 60,
            longRestDurationInput: longRestDurationInput * 60,
            autoStartTimer,
        });
    };
    const resetDefaultSettings = () => {
        dispatch("resetTimerSettings");
        const inputs = document.getElementsByTagName("input");
        for (let i = 0; i < inputs.length; i += 1) {
            inputs[i].value = "";
        }
    };
</script>

<form class="flex-container">
    <div class="grid-container">
        <h2>Settings</h2>
        <label for="work">Work time (mins):</label>
        <input
            type="number"
            id="work"
            placeholder={workDuration}
            bind:value={workDurationInput}
            disabled={timerStarted}
        />
        <label for="short-rest"> Short rest time (mins):</label>
        <input
            type="number"
            id="short-rest"
            placeholder={shortRestDuration}
            bind:value={shortRestDurationInput}
            disabled={timerStarted}
        />
        <label for="long-rest"> Long rest time (mins):</label>
        <input
            type="number"
            id="long-rest"
            placeholder={longRestDuration}
            bind:value={longRestDurationInput}
            disabled={timerStarted}
        />
        <label for="toggle-auto"
            >Auto start timer after it ends <br />
            (Manually stop the timer will deactivate this setting)
        </label>
        <input
            type="checkbox"
            id="toggle-auto"
            bind:checked={autoStartTimer}
            disabled={timerStarted}
        />
    </div>

    <div id="button-container">
        <button
            on:click|preventDefault={editTimerSettings}
            disabled={timerStarted}
        >
            Set
        </button>
        <button
            on:click|preventDefault={resetDefaultSettings}
            disabled={timerStarted}
        >
            Reset
        </button>
    </div>

    <ul>
        <li>
            <a target="_blank" href="https://icons8.com/icon/59841/moon-symbol">
                Moon Symbol
            </a>
            icon by
            <a target="_blank" href="https://icons8.com">Icons8</a>
        </li>
        <li>
            <a target="_blank" href="https://icons8.com/icon/60002/sun">
                Sun
            </a>
            icon by
            <a target="_blank" href="https://icons8.com">Icons8</a>
        </li>
        <li>
            <a
                target="_blank"
                href="https://icons8.com/icon/4511GGVppfIx/settings"
            >
                Settings
            </a>
            icon by
            <a target="_blank" href="https://icons8.com">Icons8</a>
        </li>
        <li>
            <a
                target="_blank"
                href="https://icons8.com/icon/7FSknHLAHdnP/close"
            >
                Close
            </a>
            icon by
            <a target="_blank" href="https://icons8.com">Icons8</a>
        </li>
    </ul>
</form>

<style>
    form {
        background-color: var(--theme-colors-primary_dark);
        width: 100%;
        height: 100%;
    }
    h2 {
        font-weight: 500;
    }
    button {
        width: 75px;
        padding: 8px 12px;
    }
    button:first-of-type {
        background-color: var(--theme-colors-text);
        color: var(--theme-colors-primary_dark);
        box-shadow: 0 0 10px 1px var(--theme-colors-primary);
        margin-right: 10px;
    }
    button:first-of-type:hover {
        background-color: var(--theme-colors-primary);
        color: initial;
    }

    ul {
        list-style-type: none;
        font-size: 12px;

        border-top: 1px solid;
        padding: 10px 0 0 0;
        margin: 0;
    }
    a {
        color: initial;
    }

    .flex-container {
        display: flex;
        flex-flow: column nowrap;
        justify-content: space-between;
    }

    .grid-container {
        display: grid;
        grid-template-columns: auto 150px;
        gap: 15px 20px;
    }
    .grid-container > h2 {
        grid-column: span 2;
    }
    .grid-container > label {
        align-self: center;
        text-align: left;
    }
    .grid-container > input {
        width: 100%;
        margin: 0;
        align-self: center;
        justify-self: flex-end;
    }

    #button-container {
        display: flex;
        flex-flow: row nowrap;
        justify-content: flex-end;
    }
</style>
