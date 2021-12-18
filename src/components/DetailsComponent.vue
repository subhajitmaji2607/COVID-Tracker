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
                  gridBorderColor='#90CAF9'
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
                  type="bar"
                  :graphColor="['#EF6C00']"
                  title="Daily Tested"
                  textColor='#EF6C00'
                  :xaxisTeastedGraphGraphData="xaxisTeastedGraphGraphData"
                  :teastedGraphGraphData="teastedGraphGraphData"
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
                  gridBorderColor='#BDBDBD'
                  :xaxisDeceasedGraphGraphData="xaxisDeceasedGraphGraphData"
                  :deceasedGraphGraphData="deceasedGraphGraphData"
                />
            </v-card>
        </v-col>       
    </v-row>
    <!-- {{casesTimeSeries}} -->
    <!-- {{xaxisConfirmedGraphData}} -->
    <!-- {{confirmedGraphData}} -->
    <!-- {{tested}} -->
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
        // confirmedGraphData:{
        //     graphName:'Confirm Graph',
        //     data:[]
        // },
        confirmedGraphData:[],
        xaxisRecoveredGraphData: [],
        recoveredGraphData:[],
        xaxisDeceasedGraphGraphData:[],
        deceasedGraphGraphData:[],
        xaxisTeastedGraphGraphData:[],
        teastedGraphGraphData:[]
    }),
    props: {
        casesTimeSeries:Array,
        tested:Array,
    },
    methods:{
        filterData(value){
            // console.log('call')
            // console.log(value)

            //filter data for confirm graph
            this.xaxisConfirmedGraphData = value.map((data)=>data.dateymd)
            this.confirmedGraphData = value.map((data)=>data.dailyconfirmed)

            //filter data for recover graph
            this.xaxisRecoveredGraphData = value.map((data)=>data.dateymd)
            this.recoveredGraphData = value.map((data)=>data.dailyrecovered)

            //filter data for deceased graph
            this.xaxisDeceasedGraphGraphData = value.map((data)=>data.dateymd)
            this.deceasedGraphGraphData = value.map((data)=>data.dailydeceased) 
        },
        filterTestedData(value){
            //filter data for tested graph
            this.xaxisTeastedGraphGraphData = value.map((item,index)=>this.reformatDate(item.testedasof,index))
            this.teastedGraphGraphData = value.map((item)=>item.totalsamplestested)
        },
        reformatDate (date,index){
            //this check is coz of index 42 was empty so it's coz an error
            if(index === 42){
                return '2020-04-21'
            }
            const d = date.split('/')
            return(`${d[2]}-${d[1]}-${d[0]}`)
        }
    },
    watch:{
        casesTimeSeries(value){
            // console.log('watch')
            this.filterData(value)
        },
        tested(value){
            this.filterTestedData(value)
        }
    },
    mounted(){
        // console.log('detail mounted')
        // this.filterData()

        //filter data for confirm graph
        // this.xaxisConfirmedGraphData = this.casesTimeSeries.map((data)=>data.dateymd)
        // this.confirmedGraphData = this.casesTimeSeries.map((data)=>data.dailyconfirmed)
        this.filterData(this.casesTimeSeries)
        this.filterTestedData(this.tested)
        //filter data for recover graph
        // this.xaxisRecoveredGraphData = this.casesTimeSeries.map((data)=>data.dateymd)
        // this.recoveredGraphData = this.casesTimeSeries.map((data)=>data.dailyrecovered) 
        
        // //filter data for deceased graph
        // this.xaxisDeceasedGraphGraphData = this.casesTimeSeries.map((data)=>data.dateymd)
        // this.deceasedGraphGraphData = this.casesTimeSeries.map((data)=>data.dailydeceased) 
    }
}
</script>
