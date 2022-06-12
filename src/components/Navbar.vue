<script>
export default {
  data() {
    return {};
  },
  methods: {
    search(e) {
      this.$emit("search", e.target.value);
      e.target.value = "";
    },
  },
};
</script>
<template>
  <div class="navbar">
    <div class="navbar_brand"><h1>Pokedex</h1></div>
    <form class="form" @submit.prevent>
      <input
        v-bind:value="this.value"
        type="text"
        placeholder="Search..."
        @change="search"
      />
      <button>Search</button>
    </form>
  </div>
</template>
<style>
@import "@/assets/Navbar.css";
</style>
