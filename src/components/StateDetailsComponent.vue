<template>
    <v-main class="pt-4">
        <v-row dense>
        <v-col cols="7" xs="12" :style="{/*border:'2px solid black'*/minHeight: '450px'}">
            <v-card height="100%"></v-card>
        </v-col>
         <v-col cols="5" xs="12" :style="{/*border:'2px solid black'*/minHeight: '450px'}">
            <v-card height="100%" style="display:flex; flex-direction: row">
                <v-col cols="5" :style="{/*border:'2px solid black'*/}">
                    <h3 class="font-weight-bold">Top districts</h3>
                    <template v-for="item in topDistrict">
                        <v-list :key="item[0]">
                            <v-list-item>
                                <v-list-item-content v-html="item[0]"></v-list-item-content>
                                <v-list-item-content v-html="item[1].active"></v-list-item-content>
                            </v-list-item>
                        </v-list>
                    </template>
                </v-col>
                <v-col cols="7" :style="{/*border:'2px solid black'*/}">
                    <BarGraph :topDistrictGraphData="topDistrictGraphData"/>
                </v-col>
            </v-card>
        </v-col>
    </v-row>
    <!-- {{selectedState}} -->
    <!-- {{topDistrict}} -->
    </v-main>
</template>

<script>
import BarGraph from './graph/BarGraph.vue'
export default {
    name:'StateDetails',
    components:{
        BarGraph
    },
    props:{
        district_data:Object,
        selectedState:String,
    },
    data:()=>({
        topDistrict:[],
        topDistrictGraphData:[],
    }),
    methods:{
        getTopDistrict(data,state){
            console.log(state)
            // console.log(data)
            Object.entries(data).forEach(([key,value])=>{
                // console.log(key,value)
                if(key === state){
                    this.topDistrict = (Object.entries(value.districtData).sort((a,b)=>b[1].active - a[1].active)).slice(0,4)
                    this.topDistrictGraphData = this.topDistrict.map((ele)=>ele[1].active)
                }
            })
        }
    },
    mounted(){
        // console.log('datails mounted')
        // console.log(this.selectedState)
        // console.log(this.district_data)
        this.getTopDistrict(this.district_data,this.selectedState)
    },
    watch:{
        selectedState(stateName){
            // console.log(value)
            this.getTopDistrict(this.district_data,stateName)
        }
    }
}
</script>