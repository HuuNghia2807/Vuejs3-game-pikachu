<template>
    <div class="card" :class="{ disabled: isDisabled }">
        <div
            class="card__inner"
            :class="{ 'is-flipped': isFlipped }"
            @click="onToggleFlipCard"
        >
            <div class="card__face card__face--front">
                <div class="card__content"></div>
            </div>
            <div class="card__face card__face--back">
                <div
                    class="card__content"
                    :style="{
                        backgroundImage: `url(${
                            '/src/assets/' + imgBackFaceUrl
                        })`,
                    }"
                ></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        imgBackFaceUrl: {
            type: String,
            required: true,
        },
        card: {
            type: [String, Number, Array, Object]
        }
    },
    data() {
        return {
            isFlipped: false,
            isDisabled: false,
        };
    },
    methods: {
        onToggleFlipCard() {
            if(this.isDisabled) return false;
            this.isFlipped = !this.isFlipped;
            if(this.isFlipped) this.$emit('onFlip', this.card);
        },

        onBackFlipCard: function() {
            this.isFlipped = false
        },
        
        onDisabledCard() {
            this.isDisabled = true
        }
    },
};
</script>

<style lang="css" scoped>
.card {
    display: inline-block;
    margin-right: 1rem;
    margin-bottom: 1rem;
    height: 120px;
    width: 90px;
}

.card.disabled .card__inner {
    cursor: default;
}
.card__inner {
    width: 100%;
    height: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
    cursor: pointer;
    position: relative;
}
.card__inner.is-flipped {
    transform: rotateY(-180deg);
}

.card__face {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    overflow: hidden;
    border-radius: 1rem;
    padding: 1rem;
    box-shadow: 0 3px 10px 2px #ccc;
}

.card__face--front .card__content {
    background: url("../assets/imgs/icon_back.png") no-repeat center center;
    background-size: 40px 40px;
    height: 100%;
    width: 100%;
}

.card__face--back {
    background-color: var(--white);
    transform: rotateY(-180deg);
}

.card__face--back .card__content {
    background-size: contain;
    background-position: center center;
    background-repeat: no-repeat;
    height: 100%;
    width: 100%;
}
</style>
