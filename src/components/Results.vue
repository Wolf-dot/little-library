<template>
  <article>
    <div class="result" v-for="result in results" :key="result.show.id">
      <div v-if="result.show.image">
        <img :src="result.show.image.medium" alt="show cover" />
      </div>
      <div v-else>
        <div class="rectangle">no image</div>
      </div>
      <h3>
        {{ result.show.name }}
      </h3>
      <p>
        <mark v-if="result.show.rating.average">
          {{ result.show.rating.average }}
        </mark>
      </p>
      <mark @click="showMore(result)">More info</mark>
    </div>
  </article>
</template>

<script>
export default {
    name: "Results",
    props:{
        results: Object
    }
}
</script>

<style scoped>
@import "../assets/shows.css";
</style>