<script>
import axios from "axios";
import ListPokemon from "./components/ListPokemon.vue";
import ModalWindowVue from "./components/ModalWindow.vue";
import ModalWindow from "./components/ModalWindow.vue";
import Navbar from "./components/Navbar.vue";
import FoundCard from "./components/FoundCard.vue";
export default {
  components: {
    ListPokemon,
    ModalWindowVue,
    ModalWindow,
    Navbar,
    FoundCard,
  },
  data() {
    return {
      cards: [],
      card: null,
      page: 1,
      limit: 6,
      offset: 0,
      isShow: false,
      isShowCard: false,
      info: null,
      isLoad: false,
    };
  },

  methods: {
    search(name) {
      this.fetchCard(name);
    },
    // тут открывается окошка с инфой о покемоне
    openModal(info) {
      this.isShow = true;
      this.info = info;
    },
    // тут меняется страница
    changePage(direction) {
      if (this.isLoad) return;

      if (this.cards.next !== null && direction === "next") {
        this.offset += this.limit;
        this.page++;
      }

      if (this.cards.previous !== null && direction === "previous") {
        this.offset -= this.limit;
        this.page--;
      }
      this.saveData();
    },

    //тут они сохраняются
    saveData() {
      localStorage.clear();
      localStorage.setItem("page", this.page);
    },
    //данные тут выгружаются
    loadData() {
      this.page = localStorage.getItem("page")
        ? localStorage.getItem("page")
        : 1;
      this.offset = localStorage.getItem("page")
        ? (this.page - 1) * this.limit
        : 0;
    },

    // тут я получаю нужное кол во покемонов и отправляю их в компонент listPokemon оттуда уже появлются карточки с картинками и инфой , была возможность получать их по id и вызывать их через цикл но отказался от этого так как после 898id выдавала ошибку , и поэтому применяю это способ
    async fetchCards() {
      this.isLoad = true;

      try {
        const response = await axios.get("https://pokeapi.co/api/v2/pokemon", {
          params: {
            limit: this.limit,
            offset: this.offset,
          },
        });

        this.cards = response.data;
      } catch (e) {
        alert("Ошибка");
        console.log(e);
      }
      this.isLoad = false;
    },
    // тут получаю покемона который вызваются через поисковую строку
    async fetchCard(name) {
      this.isLoad = true;
      try {
        const response = await axios.get(
          `https://pokeapi.co/api/v2/pokemon/${name}/`
        );

        this.info = response.data;
        this.isShowCard = true;
      } catch (e) {
        alert("you entered the wrong pokemon name");
        console.log(e);
      }
      this.isLoad = false;
    },
  },

  mounted() {
    this.loadData();
    this.fetchCards();
  },
  watch: {
    page() {
      this.fetchCards();
    },
  },
};
</script>

<template>
  <navbar @search="search" />
  <div v-if="!isShowCard" class="container">
    <div>
      <list-pokemon @openModal="openModal" :cards="cards.results" />
    </div>
    <div class="btn_container">
      <button
        class="btn"
        :class="[this.cards.previous !== null ? 'enable' : 'disable']"
        @click="changePage('previous')"
      >
        previous
      </button>
      <div class="page_text">
        <h4>{{ page }}</h4>
      </div>
      <button
        class="btn"
        :class="[this.cards.next !== null ? 'enable' : 'disable']"
        @click="changePage('next')"
      >
        next
      </button>
    </div>
  </div>

  <found-card
    v-model:isShowCard="isShowCard"
    :cardInfo="info"
    @openModal="openModal"
  />
  <modal-window v-model:isOpen="isShow" :info="info" />
</template>

<style>
@import "@/assets/base.css";
</style>
