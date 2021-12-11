<template>
  <v-app>
    <Navigationber/>
    <v-main>
      <MainSection/>
    </v-main>
  </v-app>
</template>

<script>
import Navigationber from './components/Navigationbar.vue'
import MainSection from './components/MainSection.vue'
export default {
    name: "App",

    components: {
        Navigationber,
        MainSection,
    },

    data: () => ({
        //*
    }),
};
</script>
