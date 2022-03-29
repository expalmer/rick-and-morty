<template>
  <h1>Rick and Morty {{ name }} {{ age }}</h1>
  <button @click="total = total + 2">+</button>
  <h2>{{ total }}</h2>

  <input type="text" v-model="text" @keyup.enter="meuChange" />
  <h3>{{ text }}</h3>
  <ul>
    <li v-for="character in characters" :key="character.id">
      {{ character.name }}
      <img v-bind:src="character.image" />
      <p>{{ character.species }}</p>

      <p v-for="epi in character.episode" :key="epi">{{ epi }}</p>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      animal: "Tigre",
      age: 1,
      text: "vazio",
      characters: ["Palmer", "Leo", "Luiz", "Bia"],
    };
  },
  methods: {
    meuChange(e) {
      console.log("-->", e.target.value);
      this.characters.push(e.target.value);
      this.text = "";
    },
  },
  mounted() {
    fetch("https://rickandmortyapi.com/api/character")
      .then((response) => response.json())
      .then((response) => {
        this.characters = response.results;
      });
  },
};
</script>

<style>
h1 {
  color: red;
}
</style>
