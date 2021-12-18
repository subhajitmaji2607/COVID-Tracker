<template>
<div>
    <apexchart width="100%" height="300" :type="type" :options="options" :series="series"></apexchart>
</div>
</template>

<script>
export default {
    name: 'RecoveredGraph',
    data: function () {
        return {
            options: {
                chart: {
                    id: 'vuechart-example'
                },
                xaxis: {
                    type: 'datetime',
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
                name: 'Recovered Graph',
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
        xaxisRecoveredGraphData:Array,
        recoveredGraphData:Array
    },
    watch:{
        xaxisRecoveredGraphData(value){
            // console.log(value)
            this.options={
                xaxis:{
                    categories: value
                }
            }
        },
        recoveredGraphData(value){
            // console.log(value)
            this.series =[{
            name: 'Recovered Graph',
            data: value
        }]
        }
    },
}
</script>
