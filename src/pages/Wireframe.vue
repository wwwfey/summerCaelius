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
import LandHome from "components/wireframe/LandHome.vue";
import Sections from "components/wireframe/Sections.vue";
import Table from "components/wireframe/Table.vue";
import Cartoon from "components/wireframe/Cartoon.vue";
import Footer from "components/wireframe/Footer.vue";

</script>
<style lang="scss" scoped>

</style>