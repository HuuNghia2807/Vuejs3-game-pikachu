<template>
    <div class="screen">
        <h1 class="title">Congratulations</h1>
        <p class="result">{{ Math.round(timer / 1000) }} seconds</p>
        <p class="comment">{{ cmt }}</p>
        <button class="btn" @click="onStartAgain">
            <span class="btn__content">
                Start Again
            </span>
        </button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                cmt: 'Quá gà... !'
            }
        },
        props: {
            timer: Number
        },
        methods: {
            onStartAgain() {
                this.$emit('onStartAgain')
            }
        }
    }
</script>

<style lang="css" scoped>

.screen {
    display: flex;
    height: 100vh;
    width: 100%;
    flex-direction: column;
    background-color: var(--black-color);
    color: var(--white-color);
    justify-content: center;
    align-items: center;
}

.title {
    font-size: 7rem;
}

.result {
    font-size: 4rem;
    margin: 1rem 0 0 0;
    color: yellow;
}
.comment {
    font-size: 5rem;
    margin-bottom: 2rem;
    color: red;
    font-weight: 700;
}

.btn {
    width: 150px;
    cursor: pointer;
    background: transparent;
    color: var(--white-color);
    border: solid 2px #f3f3f3;
    margin: 0 1.5rem;
    border-radius: 1rem;
}

.btn:hover {
    background-color: #f3f3f3;
    color: var(--black-color);
}

.btn__content {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 20px 30px;
    font-size: 1.6rem;
    font-weight: 600;
}

</style>