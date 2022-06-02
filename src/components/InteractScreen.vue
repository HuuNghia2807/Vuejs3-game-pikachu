<template>
    <div class="screen">
        <div class="show-time">{{ time }}</div>
        <div
            class="screen__inner"
            :style="{
                width: `${
                    ((((920 - 23.5 * 4) / Math.sqrt(cardsContext.length) - 16) *
                        3) /
                        4 +
                        16) *
                    Math.sqrt(cardsContext.length)
                }px`,
            }"
        >
            <Card
                v-for="(card, index) in cardsContext"
                :key="index"
                :ref="`card-${index}`"
                :imgBackFaceUrl="`imgs/${card}.png`"
                :card="{ index, value: card }"
                :cardsContext="cardsContext"
                @onFlip="checkRule($event)"
                @onCloseFlip="onCloseCard($event)"
                :rules="rules"
            />
        </div>
    </div>
</template>

<script>
import Card from "./Card.vue";
export default {
    props: {
        cardsContext: {
            type: Array,
            default: function () {
                return [];
            },
        },
    },
    components: {
        Card,
    },
    data() {
        return {
            rules: [],
            time: 0,
            timeInterval: null,
        };
    },
    methods: {
        checkRule(card) {
            if (this.rules.length === 2) return false;

            this.rules.push(card);

            if (
                this.rules.length === 2 &&
                this.rules[0].value === this.rules[1].value
            ) {
                this.$refs[`card-${this.rules[0].index}`][0].onDisabledCard();
                this.$refs[`card-${this.rules[1].index}`][0].onDisabledCard();
                // cap nhat lai rule
                this.rules = [];

                const disabledElement =
                    document.querySelectorAll(".card.disabled");
                if (
                    disabledElement &&
                    disabledElement.length === this.cardsContext.length - 2
                ) {
                    setTimeout(() => {
                        clearInterval(this.timeInterval);
                        this.$emit("onFinish");
                    }, 1000);
                }
            } else if (
                this.rules.length === 2 &&
                this.rules[0].value !== this.rules[1].value
            ) {

                this.$refs[`card-${this.rules[0].index}`][0].onDisabledCard();
                this.$refs[`card-${this.rules[1].index}`][0].onDisabledCard();
                setTimeout(() => {
                    // Dong 2 card lai
                    this.$refs[
                        `card-${this.rules[0].index}`
                    ][0].onBackFlipCard();
                    this.$refs[
                        `card-${this.rules[1].index}`
                    ][0].onBackFlipCard();
                    // cap nhat lai rule
                    this.$refs[
                        `card-${this.rules[0].index}`
                    ][0].onEnabledCard();
                    this.$refs[
                        `card-${this.rules[1].index}`
                    ][0].onEnabledCard();

                    this.rules = [];
                }, 800);
            } else return false;
        },
        onCloseCard(card) {
            this.$refs[`card-${this.rules[0].index}`][0].onBackFlipCard();
            this.rules.pop();
        },
        start() {
            this.timeInterval = setInterval(() => {
                this.time++;
            }, 1000);
        },
    },
    mounted() {
        this.start();
    }
};
</script>

<style lang="css" scoped>
.screen {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100vh;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 2;
    background-color: var(--black-color);
    color: var(--white-color);
}

.show-time {
    font-size: 4rem;
}

.screen__inner {
    display: flex;
    flex-wrap: wrap;
    margin: 2rem auto;
}
</style>
