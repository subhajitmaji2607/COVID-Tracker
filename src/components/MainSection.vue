<template>
<v-container fluid>
    <v-row dense class="mt-1">
        <v-row dense class="mt-1 ml-4">
            <v-col cols="12" sm="3">
                <GeneralCard color='#D1C4E9' icon='trending_up' iconColor='#6A1B9A' cardTitle="Confirmed" :data="stateInfo.confirmed"/> <!--deep-purple lighten-4 -->
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#BBDEFB" icon="masks" iconColor="#1565C0" cardTitle="Active" :data="stateInfo.active"/> <!--blue lighten-4-->
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#C5E1A5" icon="favorite" iconColor="#1B5E20" cardTitle="Recoverd" :data="stateInfo.recovered"/> <!--green lighten-3--->
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#EEEEEE" icon="local_florist" iconColor="#616161" cardTitle="Death" :data="stateInfo.deaths"/> <!--grey lighten-3-->
            </v-col>
        </v-row>
        <v-col cols="12" sm="3" class="mt-2">
            <v-select :items="statesName" v-model="selectedState" :hint="stateInfo.lastupdatedtime" label="Location" outlined prepend-inner-icon="location_on" menu-props="auto"></v-select>
        </v-col>
    </v-row>
    <!-- <p>{{ selectedState }}</p>-->
    <!-- <p>{{ stateInfo }}</p> -->
</v-container>
</template>

<script>
import GeneralCard from './GeneralCard.vue'
import axios from 'axios'
export default {
    name: 'Body',
    components: {
        GeneralCard,
    },
    data: () => ({
        items: ['Foo', 'Bar', 'Fizz', 'Buzz'],
        data:{
            total: 5000,
            active:500,
            recoverd:4300,
            death:200
        },
        statewiseData:[],
        statesName:[],
        selectedState: 'All',
        stateInfo:{},
    }),
    async mounted(){
        const {data} = await axios.get('https://data.covid19india.org/data.json')
        this.statewiseData = data.statewise
        this.stateInfo = this.statewiseData[0]
        // console.log(data.statewise)
    },
    //watcher are execute when the value of a 
    watch:{
        statewiseData(states){
            this.statesName = states.map((state)=>{
                if(state.state === 'Total'){
                    return 'All'
                }
                else{
                    return state.state
                }
            })
        },
        selectedState(stateName){
            if(stateName === 'All') this.stateInfo = this.statewiseData[0]
            else this.stateInfo = this.statewiseData.filter((state)=>state.state === stateName)[0]
        }
    },
    // methods:{
    //     extractStatenameFromstatewiseDataIntoAnArray(data){
    //        this.statesName =  data.map((state)=>{
    //            state.state
    //         })
    //     }
    // }
}
</script>
