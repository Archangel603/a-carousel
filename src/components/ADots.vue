<template>

    <div :class="rootClass">
        <div
                v-for="(item, index) in slides"
                :key="'dot-' + index"
                :class="{ 'a-slider-dot': true, active: index === active }"
                @click="$emit('change', index)"
        ></div>
    </div>

</template>

<script>
    export default {
        name: "Dots",

        props: {
            active: Number,
            slides: Array,
            type: {
                type: String,
                default: ""
            }
        },
        computed: {
            rootClass() {
                let className = "a-dots-trail";

                if (this.type === "rounded") {
                    className += " dots-rounded";
                }
                else if (this.type === "line") {
                    className += " dots-line";
                }

                return className;
            }
        }
    }
</script>

<style scoped lang="scss">

    .a-dots-trail {
        display: flex;
        
    }

    .a-dots-trail.dots-line {

        background: rgba(255, 255, 255, 0.4);
        border-radius: 0%;
        height: 4px;
        margin: 0 0 0.8em;

        .a-slider-dot {
            position: relative;
            width: 100%;
            padding-bottom: 1em;

            &:not(.active) {
                cursor: pointer;
            }

            &::before {
                position: absolute;
                display: block;
                content: "";
                width: 100%;
                height: 4px;
                border-radius: 10%;
                transition: .2s;
            }

            &.active::before {
                background: white;
            }

            @media all and (min-width: 961px) {
                &:hover::before {
                    background: #ddd;
                }
            }
        }
    }

    .a-dots-trail.dots-rounded {

        justify-content: center;

        .a-slider-dot {
            position: relative;
            margin: 0 5px;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.4);

            &:not(.active) {
                cursor: pointer;
            }

            &.active {
                background: white;
            }

            @media all and (min-width: 961px) {
                &:hover {
                    background: #ddd;
                }
            }
        }
    }
    

</style>