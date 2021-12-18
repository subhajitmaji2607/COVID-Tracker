<template>
<div>
    <apexchart width="100%" height="300" :type="type" :options="options" :series="series"></apexchart>
</div>
</template>

<script>
// import axios from 'axios'
export default {
    name: 'TestedGraph',
    data: function () {
        return {
            options: {
                chart: {
                    id: 'vuechart-example'
                },
                xaxis: {
                    type: 'datetime',
                    // categories: ['1991', '1992', '1993', '1994', '1995', '1996', '1997', '1998']
                    categories:[]
                },
                yaxis:{
                    show: false
                },
                colors:this.graphColor,
                dataLabels:{
                    enabled: false
                },
                grid:{
                    show:true,
                    borderColor:this.gridBorderColor,
                    xaxis:{
                        line:{
                            show: true
                        }
                    },
                },
                title:{
                    text: this.title,
                    align:'left',
                    margin: 10,
                    style:{
                        color:this.textColor,
                        fontWeight:  'bold',
                        fontSize:  '18px',
                    }
                }
            },
            series: [{
                name: 'Tested Graph',
                // data: ['30', '40', '45', '50', '49', '60', '70', '91'],
                data:[]
            }],
        }
    },
    props:{
        type: String,
        title:String,
        textColor:String,
        graphColor:Array,
        gridBorderColor:String,
        xaxisTeastedGraphGraphData:Array,
        teastedGraphGraphData:Array,
    },
    async mounted(){
        // const {data} = await axios.get('https://data.covid19india.org/data.json')
        // // console.log(data.tested.map((item)=>item.totalsamplestested))
        // // console.log(data.tested.map((item)=>(item.testedasof)))
        //  this.series =[{
        //     name: 'Tested Graph',
        //     data: data.tested.map((item)=>item.totalsamplestested)
        // }],
        // this.options={
        //     xaxis: {
        //         categories: data.tested.map((item,index)=>this.reformatDate(item.testedasof,index))
        //     },
        // }
    },
    // methods:{
    //     reformatDate (date,index){
    //         //this check is coz of index 42 was empty so it's coz an error
    //         if(index === 42){
    //             return '2020-04-21'
    //         }
    //         const d = date.split('/')
    //         return(`${d[2]}-${d[1]}-${d[0]}`)
    //     }
    // },
    watch:{
        xaxisTeastedGraphGraphData(value){
            // console.log(value)
            this.options={
                xaxis:{
                    categories: value
                }
            }
        },
        teastedGraphGraphData(value){
            // console.log(value)
            this.series =[{
            name: 'Tested Graph',
            // name: value.graphName,
            data: value
        }]
        }
    }
}
</script>
