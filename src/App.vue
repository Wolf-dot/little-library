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

  <Input @input="searchLibrary"/>
  <Suspense v-if="searching">
    <template #default>
      <Results :results="results"/>
    </template>
    <template #fallback>
      The list is loading...
    </template>
  </Suspense>
  
</template>

<script>
import Modal from './components/Modal'
import Header from './components/Header'
import Input from './components/Input'
import Results from './components/Results'

export default {
  name: 'App',
  components: {
    Header,
    Modal,
    Input,
    Results
  },
  data() {
    return {
      showModal: true,
      error: {is: false, message: "Please input name before proceeding"},
      name: "",
      searching: false,
      results: {}
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
    },
    async searchLibrary(title){
      title = title.trim()
      title = title.replaceAll(" ", "+")
      const response = await fetch("https://openlibrary.org/search.json?q=" + title)
      this.results = await response.json()
      this.searching = true
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
}
</style>
