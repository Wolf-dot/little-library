<template>
    <div class="backdrop">
        <div class="modal">
            <h2> {{ content }} </h2>
            <h3 v-if="error" class="error"> {{ err }} </h3>
            <slot></slot> 
        </div>
    </div>
</template>

<script>
export default {
    name: "Modal",
    props: {
        content: String,
        err: String,
        error: Boolean
    }
}
</script>

<style>
    .backdrop{
        top: 0px;
        position: fixed;
        background: lightgray;
        width: 100%;
        height: 100%;
    }
    .modal{
        background: white;
        width: fit-content;
        padding: 20px;
        margin: 100px auto;
        border-radius: 20px;
    }
</style>