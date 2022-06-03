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
            Reset Default
        </button>
    </div>

    <ul>
        <li>
            <a
                href="https://www.flaticon.com/free-icons/settings"
                title="settings icons"
            >
                Settings icons created by Pixel perfect - Flaticon
            </a>
        </li>
        <li>
            <a
                href="https://www.flaticon.com/free-icons/cross-mark"
                title="cross mark icons"
            >
                Cross mark icons created by Ilham Fitrotul Hayat - Flaticon
            </a>
        </li>
    </ul>
</form>

<style>
    form {
        background-color: var(--theme-colors-secondary);
        width: 100%;
        height: 100%;
    }
    h2 {
        font-weight: 500;
    }
    button {
        padding: 8px 12px;
        margin: 0;
    }
    button:first-of-type {
        margin-right: 10px;
    }
    ul {
        list-style-type: none;
        padding: 0;
        margin: 0;
    }

    .flex-container {
        display: flex;
        flex-flow: column nowrap;
        justify-content: space-evenly;
    }

    .grid-container {
        display: grid;
        grid-template-columns: auto 150px;
        gap: 15px 20px;
    }
    .grid-container > h2 {
        grid-column: span 2;

        margin: 0;
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
