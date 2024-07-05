<template>
    <div class="wrapper full-width">
      <video autoplay muted loop class="background-video" v-if="!$q.platform.is.mobile">
        <source src="~assets/seavid.mp4" type="video/mp4">
      </video>

        <div class="column justify-center text-center full-width">
          <h2 class="text-weight-bolder feeling-passionate">Hello Summer <br>
            @<br>
          Feynman</h2>

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

video {
  position: absolute;
  top: 0;
  left: 0;
  min-width: 100%;
  min-height: 100%;
  z-index:-100;
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
