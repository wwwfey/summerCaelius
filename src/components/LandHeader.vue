<template>
    <q-header reveal elevated  style=" width: 100vw">
        <q-toolbar class="flex justify-between bg-red-2">

            <router-link to="/">
                <q-toolbar-title class="row">
                    <div class="row items-baseline justify-start">
                        <div class="font-h65 text-white" style="flex: 1">
                            Ffffffey
                        </div>
                    </div>
                </q-toolbar-title>
            </router-link>

            <div class="flex items-end gt-sm q-mr-lg text-black">
                <q-btn flat to="/wireframe" label="wireframe"/>
            </div>

        </q-toolbar>
    </q-header>
</template>

<script setup>

</script>

<style scoped>

a {
    text-decoration:none;
}

.q-item.q-router-link--active, .q-item--active {
    color: white;
}

</style>
