<template>
<body>
  <table border=1 v-if="home">
    <tr>
    <th>Address</th>
    <th>Apt</th>
    <th>Year Built</th>
    <th>Longitude</th>
    <th>Latitude</th>
    <th>Neighborhood</th>
    <th>Block</th>
    <th>Lot</th>
    <th>Building Class</th>
    <th>Tax Class</th>
    </tr>
    <tr v-for="property in properties" v-bind:key="property" v-on:click="findsales(property)">
        <td>{{ property.address }}</td>
        <td>{{ property.apt }}</td>
        <td>{{ property.yr_built }}</td>
        <td>{{ property.long }}</td>
        <td>{{ property.lat }}</td>
        <td>{{ property.nbhd }}</td>
        <td>{{ property.block }}</td>
        <td>{{ property.lot }}</td>
        <td>{{ property.bldg_cls_p }}</td>
        <td>{{ property.tax_cls_p }}</td>
    </tr>
    <tr>
        <td v-on:click="getProperties(prev)"><p>&#60;--Previous</p></td>
        <td colspan="8">Showing {{start}} to {{end}} of {{count}}</td>
        <td v-on:click="getProperties(nxt)"><p v-if="nxt">Next--&#62;</p></td>
    </tr>
  </table>
  <table border=1 v-if="propertyview">
    <tr>
        <td>bbl_id</td>
        <td>address</td>
        <td>apt</td>
        <td>zip</td>
        <td>syear</td>
        <td>easmnt</td>
        <td>tax_cls_s</td>
        <td>blog_cls_p</td>
        <td>sale_date</td>
        <td>price</td>
        <td>res_unit</td>
        <td>com_unit</td>
        <td>tot_unit</td>
        <td>bldg_ctgy</td>
        <td>message</td>
    </tr>
    <tr v-for="sale in sales" v-bind:key="sale">
        <td>{{ sale.bbl_id }}</td>
        <td>{{ sale.address }}</td>
        <td>{{ sale.apt }}</td>
        <td>{{ sale.zip }}</td>
        <td>{{ sale.syear }}</td>
        <td>{{ sale.easmnt }}</td>
        <td>{{ sale.tax_cls_s }}</td>
        <td>{{ sale.blog_cls_p }}</td>
        <td>{{ sale.sale_date }}</td>
        <td>{{ sale.price }}</td>
        <td>{{ sale.res_unit }}</td>
        <td>{{ sale.com_unit }}</td>
        <td>{{ sale.tot_unit }}</td>
        <td>{{ sale.bldg_ctgy }}</td>
        <td>{{ sale.message }}</td>
    </tr>
    <tr>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
        <td><input/></td>
    </tr>
    <tr>
        <td v-on:click="propertyview=false; home=true"><p>&#60;--Back</p></td>
        <td colspan="9">Showing Sales</td>
        
    </tr>
  </table>
  </body>
</template>

<script>
import axios from 'axios'
axios.defaults.baseURL = '//68.54.138.144:8080/';
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  mounted: function () {
    this.home=true
    this.getProperties()
  },
  data: function () {
    return {
      properties: [],
      sales:[],
      count:0,
      nxt:"",
      prev:"",
      start:0,
      end:0,
      home:true,
      propertyview:false
    }
  },
  methods: {
    get: function (url) {
        console.log(url)
        return new Promise((resolve, reject) => {
            axios.get(url, {
                dataType: 'json',
                headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json',
                },
                credentials: 'include'
            })
            .then(response => {
                //console.log(JSON.stringify(response.data))
                resolve(response)
            })
            .catch(e => {
                console.log(e)
                reject(e)
            })
            })
        },
    getProperties: function (page) {
        let url='properties'
        if (page) {
            url= url + "/?"+ page
        }
        this.get(url).then(response => {
            console.log(response)
            this.properties= response.data.results
            this.count= response.data.count
            this.nxt=response.data.next.split("?")[1]
            this.prev=response.data.previous.split("?")[1]
            this.start=1+this.properties.length*parseInt(this.prev.split("=")[1])
            this.end=1+this.properties.length*(parseInt(this.prev.split("=")[1])+1)
        })
        console.log(this.nxt)
    },
    findsales: function (property) {
        this.home=false
        this.propertyview=true
        let url='property/?bbl_id='+property.bbl_id+'&address='+property.address+'&apt='+property.apt
        this.get(url).then(response => {
            console.log(response)
            this.sales= response.data.results
        })
        console.log(this.sales)
    },
    findsales2: function (property) {
        console.log(property)
        this.home=false
        this.propertyview=true
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table {
margin-left: auto;
margin-right: auto;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
