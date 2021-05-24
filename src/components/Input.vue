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

<style>
    input[type=text] {
        text-align: center;
        font-size: 1.3em;
        width: 100%;
        padding: 12px 20px;
        box-sizing: border-box;
        border: none;
        border-bottom: 2px solid olive;
    }
    button {
        border: none;
        color: white;
        margin: 10px;
        padding: 1em;
        background-color: olive;
        border-radius: 50px;
    }
</style>