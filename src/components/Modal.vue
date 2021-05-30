<template>
    <div class="backdrop">
        <div class="modal">
            <h2> {{ content }} </h2>
            <slot></slot> 
        </div>
    </div>
</template>

<script>
export default {
    name: "Modal",
    props: {
        content: String
    }
}
</script>

<style>
    .backdrop{
        top: 0px;
        position: fixed;
        background: rgba(0,0,0,.8);
        width: 100%;
        height: 100%;
    }
    .modal{
        background: #181818;
        width: fit-content;
        padding: 20px;
        margin: 100px auto;
        border-radius: 20px;
    }
</style>