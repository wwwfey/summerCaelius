<template>
  <q-page class="flex column">
    <div class="row" style="height:100vh">
      <LandHome/>
    </div>
    <div class="q-px-md-md">
      <Sections/>
      <Table/>
      <Cartoon/>
    </div>
    <Footer/>
  </q-page>
</template>

<script setup>
import LandHome from "components/LandHome.vue";
import Sections from "components/Sections.vue";
import Table from "components/Table.vue";
import Cartoon from "components/Cartoon.vue";
import Footer from "components/Footer.vue";

</script>
<style lang="scss" scoped>

</style>
