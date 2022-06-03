<script>
    import TimerTypes from "./PomoTimerTypes.svelte";
    import ThemeToggle from "./ThemeToggle.svelte";
    import SettingButton from "./SettingButton.svelte";
    import Settings from "./PomoTimerSettings.svelte";
    import WorkSessionCounter from "./WorkSessionCounter.svelte";
    import TimerDisplay from "./TimerDisplay.svelte";

    let settingsVisible = false;

    class Timer {
        constructor(label, time) {
            this.label = label;
            this.time = time; // in seconds
        }

        get timeInMins() {
            return Math.floor(this.time / 60);
        }
    }

    const DEFAULT_TIMERS = {
        work: 1500,
        shortBreak: 300,
        longBreak: 900,
    };

    let workTimer = new Timer("Work", DEFAULT_TIMERS.work);
    let shortBreakTimer = new Timer("Short Break", DEFAULT_TIMERS.shortBreak);
    let longBreakTimer = new Timer("Long Break", DEFAULT_TIMERS.longBreak);

    let timers = [workTimer, shortBreakTimer, longBreakTimer];

    let currentTimer = workTimer;
    let countDownTimer;
    let timerStarted = false;
    let workCount = 0;
    let targetWorkCount = 4;
    let autoStartTimer = false;

    $: duration = currentTimer.time;

    const startCountDownTimer = () => {
        timerStarted = true;
        countDownTimer = setInterval(() => {
            if (duration == 0) {
                if (currentTimer == workTimer) {
                    workCount += 1;
                }
                stopCountDownTimer();
                return;
            }
            duration -= 1;
        }, 1000);
    };

    const stopCountDownTimer = () => {
        timerStarted = false;
        clearInterval(countDownTimer);

        if (currentTimer == workTimer) {
            workCount += 1;
            if (workCount == targetWorkCount) {
                currentTimer = longBreakTimer;
            } else {
                currentTimer = shortBreakTimer;
            }
        } else {
            if (currentTimer == longBreakTimer) {
                workCount = 0;
            }
            currentTimer = workTimer;
        }

        if (autoStartTimer) {
            startCountDownTimer();
        }
    };

    const updateTimerSettings = (e) => {
        console.log("UPDATE");
        console.log(e.detail);
        if (!isNaN(e.detail.workDurationInput)) {
            workTimer.time = e.detail.workDurationInput;
        }
        if (!isNaN(e.detail.shortRestDurationInput)) {
            shortBreakTimer.time = e.detail.shortRestDurationInput;
        }
        if (!isNaN(e.detail.longRestDurationInput)) {
            longBreakTimer.time = e.detail.longRestDurationInput;
        }
        autoStartTimer = e.detail.autoStartTimer;
        duration = currentTimer.time;

        settingsVisible = false;
    };

    const resetTimerSettings = () => {
        console.log("RESET");
        workTimer.time = DEFAULT_TIMERS.work;
        shortBreakTimer.time = DEFAULT_TIMERS.shortBreak;
        longBreakTimer.time = DEFAULT_TIMERS.longBreak;
        duration = currentTimer.time;
    };
</script>

<div id="pomodoro-timer__{settingsVisible ? 'active' : 'inactive'}">
    <TimerTypes {timers} {timerStarted} bind:currentTimer />

    <div class="grid-container" id="timer">
        <div class="grid-item" id="toggle-theme">
            <ThemeToggle />
        </div>

        <div class="grid-item" id="toggle-settings">
            <SettingButton bind:settingsVisible />
        </div>

        {#if settingsVisible}
            <div class="grid-item" id="settings">
                <Settings
                    workDuration={workTimer.timeInMins}
                    shortRestDuration={shortBreakTimer.timeInMins}
                    longRestDuration={longBreakTimer.timeInMins}
                    {timerStarted}
                    {autoStartTimer}
                    on:updateTimerSettings={updateTimerSettings}
                    on:resetTimerSettings={resetTimerSettings}
                />
            </div>
        {:else}
            <div class="grid-item" id="work-sessions-counter">
                <WorkSessionCounter {workCount} {targetWorkCount} />
            </div>

            <div class="grid-item" id="timer-display">
                <TimerDisplay {duration} />
            </div>

            <div class="grid-item" id="timer-button">
                {#if timerStarted}
                    <button
                        on:click={() => {
                            autoStartTimer = false;
                            stopCountDownTimer();
                        }}
                    >
                        Skip Timer
                    </button>
                {:else}
                    <button on:click={startCountDownTimer}>Start Timer</button>
                {/if}
            </div>
        {/if}
    </div>
</div>

<style>
    button {
        font-size: 24px;
    }

    .grid-container {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: repeat(5, 1fr);
        grid-column-gap: 20px;
        grid-row-gap: 20px;
    }
    .grid-item {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    #pomodoro-timer__active {
        background-color: var(--theme-colors-primary_dark);
        color: var(--theme-colors-text);
        text-align: center;
        border-radius: 10px;
    }
    #pomodoro-timer__inactive {
        background-color: var(--theme-colors-background);
        color: var(--theme-colors-text);
        text-align: center;
        border-radius: 10px;
    }

    #timer {
        height: 400px;
        padding: 20px 20px 30px 20px;
        border-radius: 10px;
    }

    #toggle-theme {
        grid-area: 1 / 1 / 2 / 2;
        z-index: 1;
    }
    #work-sessions-counter {
        grid-area: 1 / 2 / 2 / 4;
    }
    #toggle-settings {
        grid-area: 1 / 4 / 2 / 5;
        z-index: 1;
    }
    #timer-display {
        grid-area: 2 / 2 / 5 / 4;
    }
    #timer-button {
        grid-area: 5 / 2 / 6 / 4;
    }

    #settings {
        grid-area: 1 / 1 / 6 / 5;
    }
</style>
