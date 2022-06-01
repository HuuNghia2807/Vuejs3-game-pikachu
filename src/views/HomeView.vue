<template>
    <div>
        <MainScreen
            v-if="statusMatch === 'default'"
            @onStart="handleBeforeStartGame"
        />
        <InteractScreen
            v-if="statusMatch === 'match'"
            :cardsContext="settings.cardsContext"
        />
    </div>
</template>

<script>
import MainScreen from "../components/MainScreen.vue";
import InteractScreen from "../components/InteractScreen.vue";

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
    },
    components: {
        MainScreen,
        InteractScreen,
    },
};
</script>
