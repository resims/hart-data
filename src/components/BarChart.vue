<template>
    <div v-if="series.length > 0">        
        <apexchart
            width="350"            
            type="bar"
            :options="chartOptions"
            :series="series"
        ></apexchart>
    </div>
</template>

<script>
    export default {
        name: 'BarChart',
        props: ['boroughpopulation', 'type'],
        data: function() {
            return {
                chartOptions: {
                    chart: {
                        id: "vuechart-example"
                    },
                    xaxis: {
                        categories: [1950, 1960, 1970, 1980, 1990, 2000, 2010, 2020]
                    },
                }       ,
                series: []         
            }
        },
        mounted() {
            console.log("props boroughpopulation", this.boroughpopulation)
            this.fillData()
        },
        methods: {
            fillData: function() {
                if(this.type == 'first' && this.boroughpopulation !== null) {
                    this.series = [{
                        name: "series-1",
                        data: [
                            this.boroughpopulation['1950'],
                            this.boroughpopulation['1960'],
                            this.boroughpopulation['1970'],
                            this.boroughpopulation['1980'],
                            this.boroughpopulation['1990'],
                            this.boroughpopulation['2000'],
                            this.boroughpopulation['2010'],
                            this.boroughpopulation['2020'],
                        ]
                    }]
                }
                if(this.type == 'second' && this.boroughpopulation !== null) {
                    this.series = [{
                        name: "series-2",
                        data: [
                            this.boroughpopulation['1950 - Boro share of NYC total'],
                            this.boroughpopulation['1960 - Boro share of NYC total'],
                            this.boroughpopulation['1970 - Boro share of NYC total'],
                            this.boroughpopulation['1980 - Boro share of NYC total'],
                            this.boroughpopulation['1990 - Boro share of NYC total'],
                            this.boroughpopulation['2000 - Boro share of NYC total'],
                            this.boroughpopulation['2010 - Boro share of NYC total'],
                            this.boroughpopulation['2020 - Boro share of NYC total'],
                        ]
                    }]
                }                
            }
        }
    }
</script>
<style>
.apexcharts-canvas {
    margin: auto;
}
</style>