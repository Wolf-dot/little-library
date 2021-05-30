<template>
  <article v-if="found">
    <div>
      <img v-if="show.image.original" :src="show.image.original" alt="" />
      <a v-if="show.officialSite" :href="show.officialSite"><mark>{{show.officialSite}}</mark></a>
    </div>
    <div>
      <h2>{{ show.name }}</h2>
      <small>{{ show.premiered }}</small> <br />
      <small class="genres" v-for="gen in show.genres" :key="gen">{{
        gen
      }}</small>
      <p v-html="show.summary"></p>
    </div>
  </article>
  <article v-else>
      <p>(╯°□°）╯︵ ┻━┻</p>
      <p class="error">not found outside TVMaze database</p>
  </article>
</template>

<script>
export default {
  name: "CloseUp",
  props: {
    item: Object,
  },
  data() {
    return {
      show: {},
      found: false
    };
  },
  async created() {
    const response = await fetch(
      "http://api.tvmaze.com/lookup/shows?imdb=" + this.item.show
    );
    this.show = await response.json();
    if(this.show !== null){
        this.found = true;
    }
    console.log(this.show);
  },
};
</script>

<style scoped>
@import "../assets/shows.css";
</style>