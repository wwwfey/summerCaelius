<template>
  <q-layout class=" ">
    <LandHeader/>
    <div class="flex column no-wrap" style="height:100vh">
      <q-page-container>
        <router-view/>
      </q-page-container>
    </div>

  </q-layout>

</template>

<script setup>
import LandHeader from "components/wireframe/LandHeader.vue";
</script>
