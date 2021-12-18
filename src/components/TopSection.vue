<template>
<v-container fluid>
    <v-row dense class="mt-1">
        <v-row dense class="mt-1">
            <v-col cols="12" sm="3">
                <GeneralCard color='#D1C4E9' icon='trending_up' iconColor='#6A1B9A' cardTitle="Confirmed" :data="stateInfo.confirmed" />
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#BBDEFB" icon="masks" iconColor="#1565C0" cardTitle="Active" :data="stateInfo.active" />
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#C5E1A5" icon="favorite" iconColor="#1B5E20" cardTitle="Recoverd" :data="stateInfo.recovered" />
            </v-col>
            <v-col cols="12" sm="3">
                <GeneralCard color="#EEEEEE" icon="local_florist" iconColor="#616161" cardTitle="Death" :data="stateInfo.deaths" />                
            </v-col>
        </v-row>
        <v-col style="display:flex;flex-direction:column;" cols="12" sm="3">
            <v-select :items="statesName" v-model="selectedState" outlined prepend-inner-icon="search" menu-props="auto"></v-select>        
        </v-col>
    </v-row>
    <div v-if="selectedState==='All'">
        <DetailsComponent :casesTimeSeries="casesTimeSeries" />
    </div>
    <div v-else>
        <StateDetails :district_data="district_data" :selectedState="selectedState"/>
    </div>
</v-container>
</template>

<script>
import GeneralCard from './GeneralCard.vue'
import DetailsComponent from './DetailsComponent.vue'
import StateDetails from './StateDetailsComponent.vue'
import axios from 'axios'
export default {
    name: 'TopSection',
    components: {
        GeneralCard,
        DetailsComponent,
        StateDetails,
    },
    props: {
       
    },
    data: () => ({
        printKeyInConsole: false,
        statewiseData: [],
        statesName: [],
        selectedState: 'All',
        stateInfo: {},
        casesTimeSeries: [],
        district_data: {},
        districtsNameOfState: [],
        selectedDistrict: '',
        districtWiseDataOfState: {}
    }),
    async mounted() {
        // console.log('mounted')
        const {
            data
        } = await axios.get('https://data.covid19india.org/data.json')
        this.statewiseData = data.statewise
        this.stateInfo = this.statewiseData[0]
        this.casesTimeSeries = data.cases_time_series
        const data_of_district = await axios.get('https://data.covid19india.org/state_district_wise.json')
        // console.log(data_of_district.data)
        this.district_data = data_of_district.data
    },
    methods: {
       
    },
    //watcher are execute when a particular value in data changes 
    //statewiseData() execute whenever statewiseData:[] update
    watch: {
        statewiseData(states) {
            this.statesName = states.map((state) => {
                if (state.state === 'Total') {
                    return 'All'
                } else {
                    return state.state
                }
            })
        },
        selectedState(stateName) {
            // console.log(stateName)
            if (stateName === 'All') this.stateInfo = this.statewiseData[0]
            else {
                this.stateInfo = this.statewiseData.filter((state) => state.state === stateName)[0]
            }
        },
    },
}
</script>

<style>
.v-text-field.v-text-field--enclosed .v-text-field__details {
    display: none;
}
</style>
