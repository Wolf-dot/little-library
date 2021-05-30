<template>
  <div v-if="showModal">
    <Modal @close="toggleModal" content="What should we call you?">
      <Input @input="toggleModal" :error="error" />
    </Modal>
  </div>

  <header>
    <Header />
    <h2>Hello, {{ this.name }}</h2>
    <p>welcome to your little library</p>
  </header>

  <main>
    <p>Search for your favourite shows:</p>
    <Input @input="searchLibrary" :error="error" />
    <HomeBtn @home="home" />

    <div v-if="airing.is">
      <div v-if="airing.shows">
        <p>Currently airing in the US</p>
        <Airing :results="airing.shows" @more="moreInfo" />
      </div>
      <div v-else>The list is loading...</div>
    </div>

    <div v-if="searching">
      <div v-if="!loading">
        <Results :results="results" @more="moreInfo" />
      </div>
      <div v-if="loading">The list is loading...</div>
    </div>

    <div v-if="upClose.is === true">
      <CloseUp :item="upClose" />
    </div>
  </main>

  <footer>
    <p>made by Wojciech Belka</p>
    <a href="https://github.com/Wolf-dot/little-library">Github</a>
  </footer>
</template>

<script>
import Modal from "./components/Modal";
import Header from "./components/Header";
import Input from "./components/Input";
import Results from "./components/Results";
import Airing from "./components/Airing";
import CloseUp from "./components/CloseUp";
import HomeBtn from "./components/HomeBtn";

export default {
  name: "App",
  components: {
    Header,
    Modal,
    Input,
    Results,
    Airing,
    CloseUp,
    HomeBtn,
  },
  data() {
    return {
      showModal: true,
      error: { is: false, message: "Please input text before proceeding" },
      name: "",
      searching: false,
      loading: true,
      upClose: { is: false, show: "" },
      results: {},
      airing: { is: true, shows: {} },
    };
  },
  methods: {
    toggleModal(text) {
      this.name = text;
      this.showModal = !this.showModal;
    },
    async searchLibrary(title) {
      this.loading = true;
      this.searching = true;
      this.upClose.is = false;
      this.airing.is = false;
      title = title.trim();
      title = title.replaceAll(" ", "+");
      const response = await fetch(
        "http://api.tvmaze.com/search/shows?q=" + title
      );
      this.results = await response.json();
      this.loading = false;
    },
    moreInfo(result) {
      console.log(result + " more info");
      this.searching = false;
      this.airing.is = false;
      this.upClose.is = true;
      this.upClose.show = result;
    },
    home() {
      this.searching = false;
      this.airing.is = true;
      this.upClose.is = false;
    },
  },
  async created() {
    var date = new Date();
    date = date.toISOString().slice(0, 10);
    const response = await fetch(
      "http://api.tvmaze.com/schedule/web?date=" + date + "&country=US"
    );
    this.airing.shows = await response.json();
  },
};
</script>

<style>
#app {
  text-align: center;
}
</style>
