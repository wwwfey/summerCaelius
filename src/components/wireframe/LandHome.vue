<template>
    <div class="wrapper bg-grey-5 full-width">
        <div class="column justify-center text-center full-width">
            <h1 class="text-weight-bolder">Section</h1>
            <h5 class="text-weight-bolder">Local Video Background</h5>
        </div>
    </div>
</template>

<script setup>
</script>

<style scoped>
.wrapper {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: absolute;
}

.background-video {
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: -1;
    opacity: 0.5;
}
</style>