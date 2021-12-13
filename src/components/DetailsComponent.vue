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
                  :xaxisConfirmedGraphData="xaxisConfirmedGraphData"
                  :confirmedGraphData="confirmedGraphData"
                />
            </v-card>
        </v-col>
        <v-col cols="6" xs="12">
            <v-card elevation="3" color="blue lighten-5" style="min-height: 300px">
                <RecoveredGraph
                  type="area"
                  :graphColor="['#1976D2']"
                  title="Daily Recovered"
                  textColor='#1976D2'
                  :xaxisRecoveredGraphData="xaxisRecoveredGraphData"
                  :recoveredGraphData="recoveredGraphData"
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
                  type="area"
                  :graphColor="['#424242']"
                  title="Daily Deceased"
                  textColor='#424242'
                  :xaxisDeceasedGraphGraphData="xaxisDeceasedGraphGraphData"
                  :deceasedGraphGraphData="deceasedGraphGraphData"
                />
            </v-card>
        </v-col>
    </v-row>
    <!-- {{casesTimeSeries.length}} -->
    <!-- {{xaxisConfirmedGraphData}} -->
    <!-- {{confirmedGraphData}} -->
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
        xaxisConfirmedGraphData: [],
        confirmedGraphData:[],
        xaxisRecoveredGraphData: [],
        recoveredGraphData:[],
        xaxisDeceasedGraphGraphData:[],
        deceasedGraphGraphData:[]
    }),
    props: {
        casesTimeSeries:Array,
    },
    methods:{
        filterData(value){
            // console.log('call')

            //filter data for confirm graph
            this.xaxisConfirmedGraphData = value.map((data)=>data.dateymd)
            this.confirmedGraphData = value.map((data)=>data.dailyconfirmed)

            //filter data for recover graph
            this.xaxisRecoveredGraphData = value.map((data)=>data.dateymd)
            this.recoveredGraphData = value.map((data)=>data.dailyrecovered)

            //filter data for deceased graph
            this.xaxisDeceasedGraphGraphData = value.map((data)=>data.dateymd)
            this.deceasedGraphGraphData = value.map((data)=>data.dailydeceased) 

        }
    },
    watch:{
        casesTimeSeries(value){
            // console.log('watch')
            this.filterData(value)
        }
    },
    mounted(){
        // console.log('detail mounted')
        // this.filterData()

        //filter data for confirm graph
        this.xaxisConfirmedGraphData = this.casesTimeSeries.map((data)=>data.dateymd)
        this.confirmedGraphData = this.casesTimeSeries.map((data)=>data.dailyconfirmed)

        //filter data for recover graph
        this.xaxisRecoveredGraphData = this.casesTimeSeries.map((data)=>data.dateymd)
        this.recoveredGraphData = this.casesTimeSeries.map((data)=>data.dailyrecovered) 
        
        //filter data for deceased graph
        this.xaxisDeceasedGraphGraphData = this.casesTimeSeries.map((data)=>data.dateymd)
        this.deceasedGraphGraphData = this.casesTimeSeries.map((data)=>data.dailydeceased) 
    }
}
</script>
