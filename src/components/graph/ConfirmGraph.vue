<template>
<div>
    <apexchart width="100%" height="300" type="area" :options="options" :series="series"></apexchart>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'ConfirmGraph',
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
                        fontSize:  '22px',
                    }
                }
            },
            series: [{
                name: 'Confirmed Graph',
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
    },
    async mounted(){
        const {data} = await axios.get('https://data.covid19india.org/data.json')
        //sending data from child compnent to parent component
        // this.getData('top')
        this.series =[{
            name: 'Confirmed Graph',
            data: data.cases_time_series.map((item)=>item.dailyconfirmed)
        }]
        this.options={
            xaxis: {
                categories: data.cases_time_series.map((item)=>item.dateymd)
            },
        }
    },
}
</script>
