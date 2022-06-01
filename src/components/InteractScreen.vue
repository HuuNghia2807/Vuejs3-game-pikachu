<template>
    <div>
        <Card
            v-for="(card, index) in cardsContext"
            :key="index"
            :ref="`card-${index}`"
            :imgBackFaceUrl="`imgs/${card}.png`"
            :card="{ index, value: card }"
            @onFlip="checkRule($event)"
        />
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
        };
    },
    methods: {
        checkRule(card) {
            if (this.rules.length === 2) return false;

            this.rules.push(card);
            console.log(card);
            if (
                this.rules.length === 2 &&
                this.rules[0].value === this.rules[1].value
            ) {
                console.log("Right....");
                this.$refs[`card-${this.rules[0].index}`][0].onDisabledCard();
                this.$refs[`card-${this.rules[1].index}`][0].onDisabledCard();
                // cap nhat lai rule
                this.rules = [];
            } else if (
                this.rules.length === 2 &&
                this.rules[0].value !== this.rules[1].value
            ) {
                console.log("Wrong....");
                setTimeout(() => {
                    // Dong 2 card lai
                    this.$refs[
                        `card-${this.rules[0].index}`
                    ][0].onBackFlipCard();
                    this.$refs[
                        `card-${this.rules[1].index}`
                    ][0].onBackFlipCard();
                    // cap nhat lai rule
                    this.rules = [];
                }, 800);
            } else return false;
        },
    },
};
</script>

<style lang="css" scoped></style>
