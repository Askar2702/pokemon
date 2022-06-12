<script>
export default {
  props: {
    isOpen: false,
    info: null,
  },
  data() {
    return {};
  },
  methods: {
    closeModal() {
      this.$emit("update:isOpen", false);
    },
  },
  watch: {
    info() {
      // console.log(this.info);
    },
  },
};
</script>

<template>
  <div
    class="modal_back"
    :class="[this.isOpen ? 'active' : '']"
    v-on:click.stop="doThis"
    @click="closeModal"
  >
    <div v-if="info !== null" class="modal_window" @click.stop>
      <div class="exit" @click="closeModal">
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
      <div class="modal_head"><h3>Info</h3></div>

      <div class="info">
        <h5>name : {{ this.info.name }}</h5>
      </div>
      <div class="info">
        <h5>abilities:</h5>
        <h5 v-for="card in this.info.abilities" :key="card.ability.name">
          {{ card.ability.name }}
        </h5>
      </div>
      <div class="info">
        <h5>base_experience : {{ this.info.base_experience }}</h5>
      </div>
      <div class="info">
        <h5>height : {{ this.info.height }}</h5>
      </div>
      <div class="info">
        <h5>weight : {{ this.info.weight }}</h5>
      </div>
      <div class="info">
        <h5>hp: {{ this.info.stats[0].base_stat }}</h5>
      </div>
      <div class="info">
        <h5>attack : {{ this.info.stats[1].base_stat }}</h5>
      </div>
      <div class="info">
        <h5>defense : {{ this.info.stats[2].base_stat }}</h5>
      </div>
      <div class="info">
        <h5>special-attack : {{ this.info.stats[3].base_stat }}</h5>
      </div>
      <div class="info">
        <h5>special-defense : {{ this.info.stats[4].base_stat }}</h5>
      </div>
      <div class="info">
        <h5>speed : {{ this.info.stats[5].base_stat }}</h5>
      </div>
      <div class="info">
        <h5>types :</h5>
        <h5 v-for="card in this.info.types" :key="card.type.name">
          {{ card.type.name }}
        </h5>
      </div>
    </div>
  </div>
</template>

<style>
@import "@/assets/modalWindow.css";
</style>
