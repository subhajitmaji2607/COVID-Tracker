<template>
<div>
    <apexchart width="100%" height="450" type="bar" :options="options" :series="series"></apexchart>
</div>
</template>

<script>
export default {
    name: 'BarGraph',
    data: function () {
        return {
            options: {
                chart: {
                    id: 'vuechart-example'
                },
                xaxis: {
                    // type: 'datetime',
                    // categories: ['1991', '1992', '1993', '1994']
                    show: false
                },
                yaxis:{
                    show: false
                },
                colors:['#1976D2'],
            },
            series: [{
                name: 'Graph',
                data:[]
            }],
        }
    },
    props:{
        topDistrictGraphData:Array
    },
    watch:{
        topDistrictGraphData(value){
            this.series=[{
                name: 'Graph',
                data: value,
            }]
        }
    }
}
</script>
