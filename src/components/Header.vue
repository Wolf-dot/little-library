<template>
    <div class="header">
        <h3>Hello, {{ name }}.</h3>
        <h1>Welcome to your Little Library</h1>        
    </div>
</template>

<script>
export default {
    name: 'Header',
    props: {
        name: String
    }
}
</script>

<style>


</style>