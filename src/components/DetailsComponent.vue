<template>
<v-main class="pt-4">
    <v-row dense>
        <v-col cols="6" xs="12">
            <v-card elevation="3" color="red lighten-5" style="min-height: 300px">
                <ConfirmGraph
                  type="area"
                  :graphColor="['#C62828']"
                  title="Daily Confirmed"
                  textColor='#EF5350'
                  gridBorderColor='#EF9A9A'
                />
            </v-card>
        </v-col>
        <v-col cols="6" xs="12">
            <v-card elevation="3" color="green lighten-5" style="min-height: 300px">
                <RecoveredGraph
                  type="bar"
                  :graphColor="['#2E7D32']"
                  title="Daily Recovered"
                  textColor='#2E7D32'
                />
            </v-card>
        </v-col>
    </v-row>
    <v-row dense class="mt-2">
        <v-col cols="6" xs="12">
            <v-card elevation="3" color="orange lighten-5" style="min-height: 300px">
                <TestedGraph
                  type="area"
                  :graphColor="['#EF6C00']"
                  title="Daily Tested"
                  textColor='#EF6C00'
                />
            </v-card>
        </v-col>
        <v-col cols="6" xs="12">
            <v-card elevation="3" color="grey lighten-4" style="min-height: 300px">
                <DeceasedGraph
                  type="line"
                  :graphColor="['#424242']"
                  title="Daily Deceased"
                  textColor='#424242'
                />
            </v-card>
        </v-col>
    </v-row>
</v-main>
</template>

<script>
import ConfirmGraph from './graph/ConfirmGraph.vue'
import RecoveredGraph from './graph/RecoverdGraph.vue'
import DeceasedGraph from './graph/DeceasedGraph.vue'
import TestedGraph from './graph/TestedGraph.vue'
export default {
    name: 'DetailsComponent',
    components: {
        ConfirmGraph,
        RecoveredGraph,
        DeceasedGraph,
        TestedGraph,
    },
    data: () => ({
        xaxisDataForConfirmedGraph: [],
        dataForConfirmedGraph:[],
    }),
    props: {
        
    },
    // methods: {
    //     filterDataForConfirmedGraph(data) {
    //         console.log(data)
    //     }
    // },
    // mounted() {
    //     // this.filterDataForConfirmedGraph(this.data)
    //     this.xaxisDataForConfirmedGraph = this.data
    //     console.log('call')
    // },
    // watch:{
    //     rawDataForGraph(graphData){
    //         // console.log('data update')
    //         this.xaxisDataForConfirmedGraph = graphData.map((data)=>data.dateymd)
    //         this.dataForConfirmedGraph = graphData.map((data)=>data.dailyconfirmed)
    //     }
    // }
}
</script>
