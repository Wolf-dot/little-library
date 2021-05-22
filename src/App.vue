<template>
  <Header :name="name" />
  <div v-if="showModal">
    <Modal
    @close="toggleModal"
    :err="error.message"
    content="What should we call you?"
    :error="error.is">
      <Input @input="toggleModal"/>
    </Modal>    
  </div>
</template>

<script>
import Modal from './components/Modal.vue'
import Header from './components/Header.vue'
import Input from './components/Input.vue'

export default {
  name: 'App',
  components: {
    Header,
    Modal,
    Input
  },
  data() {
    return {
      showModal: true,
      error: {is: false, message: "Please input name before proceeding"},
      name: ""
    }
  },
  methods: {
    toggleModal(text){
      if(text === ""){
        this.error.is = true
      }else{
        this.name = text
        this.showModal = !this.showModal        
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
