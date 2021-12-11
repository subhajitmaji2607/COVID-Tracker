<template>
  <v-app>
    <Navigationber/>
    <v-main>
      <TopSection/>
    </v-main>
  </v-app>
</template>

<script>
import Navigationber from './components/Navigationbar.vue'
import TopSection from './components/TopSection.vue'
export default {
    name: "App",

    components: {
        Navigationber,
        TopSection,
    },

    data: () => ({
        //*
    }),
};
</script>
