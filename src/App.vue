<template>
  <v-app>
    <Navigationber/>
    <v-main>
      <TopSection :getData="getData"/>
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
    methods:{
      //getting data from child compnent into parent component
      getData(txt){
        console.log(txt)
      }
    }
};
</script>
