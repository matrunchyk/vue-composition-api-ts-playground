<template>
  <div
    id="app"
    class="characters"
  >
    <div
      v-for="(character, index) in characters"
      :key="index"
      class="character"
    >
      {{ character.name }}
    </div>
  </div>
</template>

<script lang="ts">
import { createComponent, ref } from '@vue/composition-api';
import CharacterService from '@/services/CharacterService';
// eslint-disable-next-line no-unused-vars
import Character from '@/interfaces/Character';

export default createComponent({
  setup() {
    const characterService = new CharacterService();
    const characters = ref<Character[]>([]);

    const fetchData = async (): Promise<void> => {
      console.log(characters.value);
      characters.value = await characterService.FetchCharacters();
    };

    fetchData();
    console.log(fetchData);

    return {
      characters,
    };
  },
});
</script>

<style>
  #app {
    font-family             : 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing  : antialiased;
    -moz-osx-font-smoothing : grayscale;
    text-align              : center;
    color                   : #2c3e50;
    margin-top              : 60px;
  }

  .characters {
    display           : grid;
    grid-auto-columns : auto;
  }
</style>
