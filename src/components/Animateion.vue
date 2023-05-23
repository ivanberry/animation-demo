<template>
    <div ref="numberContainer" class="number-container">{{ displayNumber }}</div>
</template>

<script>
import { gsap } from 'gsap';

export default {
    name: "animation",
    props: {
        number: {
            type: Number,
            required: true,
        },
        time: {
            type: Number,
            required: true,
        },
        step: {
            type: Number,
            required: true,
        },
    },
    data() {
        return {
            displayNumber: 0,
        };
    },
    watch: {
        number() {
            this.animateNumber();
        },
    },
    methods: {
        animateNumber() {
            this.displayNumber = 0
            gsap.to(this, {
                duration: this.time,
                displayNumber: this.number,
                ease: 'none',
                onUpdate: () => {
                    this.displayNumber = Math.floor(this.displayNumber);
                },
                step: this.step,
            });
        },
    },
};
</script>

<style>
.number-container {
    font-size: 2rem;
}
</style>