<template>
<v-main class="pt-6">
   <v-row dense>
       <v-col cols="6" xs="12">
           <v-card elevation="3" color="red lighten-4" style="min-height: 300px">
               <Graph type="area" :graphColor="['#C62828']" title="Confirmed" textColor='#EF5350' />
           </v-card>
       </v-col>
       <v-col cols="6" xs="12">
           <v-card elevation="3" color="blue-grey lighten-4" style="min-height: 300px">

           </v-card>
       </v-col>
   </v-row>
   <v-row dense class="mt-2">
       <v-col cols="6" xs="12">
           <v-card elevation="3" color="green lighten-4" style="min-height: 300px">

           </v-card>
       </v-col>
       <v-col cols="6" xs="12">
           <v-card elevation="3" color="grey lighten-4" style="min-height: 300px">

           </v-card>
       </v-col>
   </v-row>
</v-main>
</template>

<script>
import Graph from './graph/GraphComponent.vue'
export default {
    name: 'DetailsComponent',
    components:{
        Graph,
    }
}
</script>