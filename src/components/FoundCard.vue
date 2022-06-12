<template>
  <div
    class="modal_back"
    :class="[this.isShowCard ? 'active' : '']"
    v-on:click.stop="doThis"
    @click="closeModal"
  >
    <div
      @click="$emit('openModal', cardInfo)"
      @click.stop
      v-if="this.cardInfo != null"
      :class="['card', this.cardInfo.types[0].type.name]"
    >
      <div class="exit" @click="closeModal" @click.stop>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          fill="currentColor"
          class="bi bi-x-circle-fill"
          viewBox="0 0 16 16"
        >
          <path
            d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293 5.354 4.646z"
          />
        </svg>
      </div>
      <div class="name_pokemon">
        <h4>{{ this.cardInfo.name }}</h4>
        <h4>#{{ this.cardInfo.id.toString().padStart(3, 0) }}</h4>
      </div>
      <div class="img_container">
        <img
          class="img_pokemon"
          :src="this.cardInfo.sprites.front_default"
          alt="none photo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    cardInfo: null,
    isShowCard: false,
  },
  data() {
    return {};
  },
  methods: {
    closeModal() {
      this.$emit("update:isShowCard", false);
    },
  },

  mounted() {
    console.log(this.cardInfo);
  },
};
</script>

<style>
@import "@/assets/foundCard.css";
@import "@/assets/card.css";
</style>
