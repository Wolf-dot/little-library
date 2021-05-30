<template>
  <article>
    <div
      class="result"
      v-for="result in results"
      :key="result._embedded.show.id"
    >
      <div v-if="result._embedded.show.image">
        <img :src="result._embedded.show.image.medium" alt="show cover" />
      </div>
      <div v-else>
        <div class="rectangle">no image</div>
      </div>
      <h3>
        {{ result._embedded.show.name }}
      </h3>
      <p>
        <mark v-if="result._embedded.show.rating.average">
          {{ result._embedded.show.rating.average }}
        </mark>
      </p>
      <mark @click="showMore(result)">More info</mark>
    </div>
  </article>
</template>

<script>
export default {
  name: "Airing",
  props: {
    results: Object,
  },
  methods: {
    showMore(result) {
      console.log("this is hsow more " + result._embedded.show.externals.imdb);
      this.$emit("more", result._embedded.show.externals.imdb);
    },
  },
};
</script>

<style scoped>
@import "../assets/shows.css";
</style>