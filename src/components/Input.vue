<template>
  <input type="text" name="text" id="text" v-model="text" /> <br />
  <p v-if="error.is" class="error">{{ error.message }}</p>
  <button @click.prevent="submit">OK</button>
</template>

<script>
export default {
  name: "Input",
  emits: ["input"],
  props: {
    error: Object,
  },
  data() {
    return {
      text: "",
    };
  },
  methods: {
    submit() {
      if (this.text === "") {
        this.$props.error.is = true;
      } else {
        this.$props.error.is = false;
        this.$emit("input", this.text);
      }
    },
  },
};
</script>
