<template>
    <div class="screen">
        <h1 class="title">POKE MEMORIES</h1>
        <h3 class="heading">Select mode to start game</h3>
        <div class="actions">
            <button class="btn" @click="onStart({ totalBlock: 16 })">
                <div class="btn__content">
                    <span>4x4</span>
                    <span>Easy</span>
                </div>
            </button>
            <button class="btn" @click="onStart({ totalBlock: 36 })">
                <div class="btn__content">
                    <span>6x6</span>
                    <span>Normal</span>
                </div>
            </button>
            <button class="btn" @click="onStart({ totalBlock: 64 })">
                <div class="btn__content">
                    <span>8x8</span>
                    <span>Hard</span>
                </div>
            </button>
            <button class="btn" @click="onStart({ totalBlock: 100 })">
                <div class="btn__content">
                    <span>10x10</span>
                    <span>SuperHard</span>
                </div>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        onStart(config) {
            this.$emit("onStart", config);
        },
    },
};
</script>

<style lang="css" scoped>
.screen {
    background-color: var(--black-color);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    height: 100vh;
    color: var(--white-color);
}

.title {
    font-size: 8rem;
}

.heading {
    font-size: 4rem;
    margin-bottom: 3rem;
}

.actions {
    display: flex;
    justify-content: space-between;
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
    padding: 40px 40px;
}

.btn__content span {
    font-size: 2rem;
    font-weight: 600;
}
</style>
