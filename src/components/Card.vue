<template>
  <div
    @click="$emit('openModal', info)"
    v-if="this.info != null"
    :class="['card_pokemon', this.info.types[0].type.name]"
  >
    <div class="name_pokemon">
      <h4>{{ this.info.name }}</h4>
      <h4>#{{ this.info.id.toString().padStart(3, 0) }}</h4>
    </div>
    <div class="img_container">
      <img
        class="img_pokemon"
        :src="this.info.sprites.front_default"
        alt="none photo"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    cardInfo: null,
  },
  data() {
    return {
      info: null,
    };
  },
  methods: {
    // тут получаю инфу о самой карте через запрос с предоставленной url адресом
    async fetchInfo() {
      try {
        const response = await axios.get(this.cardInfo.url);
        this.info = response.data;
      } catch (e) {
        alert(e.messages);
      }
    },
  },

  mounted() {
    this.fetchInfo();
  },
};
</script>

<style>
@import "@/assets/card.css";
</style>
