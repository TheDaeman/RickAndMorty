<template>
    <section>
        <div class="characters container">
            <div class="characters__item" v-for="character in characters" :key="character.id">
                <CardCharacter :character="character"/>

            </div>
        </div>
    </section>
</template>
<script>
import { onMounted, computed } from 'vue';
import { useStore } from 'vuex';
import CardCharacter from './CardCharacter.vue';
export default {
    setup() {
        const store = useStore();
        const characters = computed(() => {
            return store.state.charactersFilter;
        });
        onMounted(() => {
            store.dispatch("getCharacters"); //Para acceder a las actions
        });
        return {
            characters
        };
    },
    components: { CardCharacter }
}
</script>
<style >
.characters{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 3rem;
    margin: 3rem 0;
}
</style>