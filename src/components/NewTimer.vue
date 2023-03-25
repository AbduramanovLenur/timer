<template>
    <li class="new-timer" @click="$emit('addComponentTimer')">
        <div class="new-timer__add">
            <span></span>
            <span></span>
        </div>
    </li>
</template>

<script>
export default {
    name: 'NewTimer'
}
</script>

<style lang="scss" scoped>
.new-timer {
    width: var(--width-timer);
    height: var(--height-timer);
    background-color: var(--grey);
    cursor: pointer;
    &__add {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        cursor: pointer;
        transition: 0.5s;
        span {
            position: absolute;
            height: 3px;
            width: 20px;
            background-color: var(--color);
            transition: 0.5s;
            &:first-child {
                transform: rotate(90deg);
            }
        }
    }
}
@media (hover: hover) {
    .new-timer {
        &__add {
            &:hover {
                span {
                    --color: #fff;
                }
            }
        }
    }
}
</style>