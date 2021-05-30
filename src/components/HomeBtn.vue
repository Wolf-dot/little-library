<template>
  <button type="button" @click="home">home</button>
</template>

<script>
export default {
    name: "HomeBtn",
    methods: {
        home(){
            this.$emit('home')
        }
    }
}
</script>