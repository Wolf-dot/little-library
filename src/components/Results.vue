<template>
    <div class="results">
        <div v-for="result in results.docs" :key="result.cover_i">
            {{result.title}}
        </div> 
    </div>  
</template>

<script>
export default {
    name: "Results",
    props:{
        results: Object
    }
}
</script>

<style>

</style>