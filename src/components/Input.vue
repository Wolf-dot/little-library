<template>
  <input type="text" name="text" id="text" v-model="text">
  <button @click.prevent="submit">OK</button>
</template>

<script>
export default {
    name: "Input",
    emits: ['input'],
    data(){
        return{
            text: ""
        }
    },
    methods: {
        submit(){
            this.$emit('input', this.text)
        }
    }
}
</script>
