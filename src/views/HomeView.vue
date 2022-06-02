<template>
    <div>
        <MainScreen
            v-if="statusMatch === 'default'"
            @onStart="handleBeforeStartGame($event)"
        />
        <InteractScreen
            v-if="statusMatch === 'match'"
            :cardsContext="settings.cardsContext"
            @onFinish="onGetResult($event)"
        />
        <ResultScreen 
            v-if="statusMatch === 'result'"
            :timer="timer"
            @onStartAgain="handleRestart"
        />
    </div>
</template>

<script>
import MainScreen from "../components/MainScreen.vue";
import InteractScreen from "../components/InteractScreen.vue";
import ResultScreen from "../components/ResultScreen.vue";

import { shuffled } from "../utils/Array";

export default {
    data() {
        return {
            statusMatch: "default",
            settings: {
                totalBlock: 0,
                cardsContext: [],
                startedAt: null,
            },
            timer: 0,
        };
    },
    methods: {
        handleBeforeStartGame(config) {
            this.settings.totalBlock = config.totalBlock;

            const firstCards = Array.from(
                { length: this.settings.totalBlock / 2 },
                (_, i) => i + 1
            );
            const secondCards = [...firstCards];
            const cards = [...firstCards, ...secondCards];

            this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));

            this.settings.startedAt = new Date().getTime();

            this.statusMatch = "match";
        },
        onGetResult() {
            // get timer
            this.timer = new Date().getTime() - this.settings.startedAt

            // chuyen qua trang result
            this.statusMatch = 'result'
        },
        handleRestart() {
            this.statusMatch = 'default'
        }
    },
    components: {
        MainScreen,
        InteractScreen,
        ResultScreen
    },
};
</script>
