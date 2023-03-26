<template>
    <li class="timer-item-s">
        <div class="timer-item-s__box">
            <div class="timer-item-s__time" :class="{ 'is-active': isActive }">
                {{ hours }} : {{ minutes }} : {{ seconds }}
            </div>
            <div class="timer-item-s__controls">
                <div class="timer-item-s__trigger">
                    <span class="timer-item-s__start" @click="start()"
                        :class="{ 'is-hide': isHide, 'is-active': isActive }"></span>
                    <span class="timer-item-s__pause" @click="stop()" :class="{ 'is-hide': !isHide, 'is-active': isActive }">
                        <span></span>
                        <span></span>
                    </span>
                </div>
                <div class="timer-item-s__trigger">
                    <span class="timer-item-s__reset" @click="reset()" :class="{ 'is-active': isActive }"></span>
                </div>
            </div>
        </div>
    </li>
</template>

<script>
export default {
    name: 'TimerItemS',
    data: () => ({
        interval: null,
        sec: 0,
        seconds: `00`,
        minutes: `00`,
        hours: `00`,
        isHide: false,
        isActive: false
    }),
    methods: {
        timer() {
            this.sec++;

            this.hours = Math.floor(this.sec / 3600);
            this.minutes = Math.floor((this.sec - (this.hours * 3600)) / 60);
            this.seconds = this.sec % 60;

            if (this.hours < 10) this.hours = `0${this.hours}`;
            if (this.minutes < 10) this.minutes = `0${this.minutes}`;
            if (this.seconds < 10) this.seconds = `0${this.seconds}`;
        },
        start() {
            if (this.interval) {
                return
            }

            this.interval = setInterval(this.timer, 1000);
            this.isHide = true;
            this.isActive = true;
        },
        stop() {
            clearInterval(this.interval);
            this.interval = null;
            this.isHide = false;
        },
        reset() {
            this.stop();
            this.sec = 0;
            this.seconds = `00`;
            this.minutes = `00`;
            this.hours = `00`;
            this.isHide = false;
            this.isActive = false;
        }
    },
}
</script>

<style lang="scss" scoped>
.timer-item-s {
    &__box {
        width: var(--width-timer);
        height: var(--height-timer);
        background-color: var(--grey);
    }
    &__time {
        --border-color: #9E9E9E;

        display: flex;
        justify-content: center;
        align-items: center;
        border-bottom: 1px solid var(--border-color);
        padding: var(--padding);
        color: var(--color);
        &.is-active {
            --border-color: #fff;
            --color: #fff;
        }
    }
    &__controls {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 50px;
        padding: var(--padding);
    }

    --height: 20px;
    --width: 20px;

    &__trigger {
        display: flex;
        justify-content: center;
        align-items: center;
        height: var(--height);
        width: var(--width);
        cursor: pointer;
    }
    &__start,
    &__pause {
        display: block;
        &.is-hide {
            display: none;
        }
    }
    &__start,
    &__pause,
    &__reset {
        &.is-active {
            --color: #fff;
        }
    }
    &__start {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
        background: var(--color);
        transform: rotate(-90deg);
        &::after {
            content: '';
            position: absolute;
            border: 10px solid transparent;
            border-top: 17px solid var(--color);
        }
    }
    &__pause {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 5px;
        span {
            display: inline-block;
            width: 3px;
            height: var(--height);
            background-color: var(--color);
        }
    }
    &__reset {
        width: 100%;
        height: 100%;
        background-color: var(--color);
    }
}
</style>