<template>
  <div class="list_pokemon">
    <Card
      @openModal="getInfo"
      v-for="card in cards"
      :cardInfo="card"
      :key="card.name"
    />
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  components: { Card },
  props: {
    cards: {
      type: Array,
      required: true,
    },
  },
  data() {},
  methods: {
    getInfo(info) {
      this.$emit("openModal", info);
    },
  },
};
</script>

<style>
@import "@/assets/listPokemon.css";
</style>
