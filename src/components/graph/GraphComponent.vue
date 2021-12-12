<template>
<div>
    <apexchart width="100%" height="300" :type="type" :options="options" :series="series"></apexchart>
</div>
</template>

<script>

export default {
    name: 'Graph',
    data: function () {
        return {
            options: {
                chart: {
                    id: 'vuechart-example'
                },
                xaxis: {
                    categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998]
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
                    borderColor:'#EF9A9A',
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
                name: 'series-1',
                data: [30, 40, 45, 50, 49, 60, 70, 91]
            }]
        }
    },
    props:{
        type: String,
        title:String,
        textColor:String,
        graphColor:Array,
    }
}
</script>
