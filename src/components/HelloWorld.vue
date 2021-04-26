<template><body>
  <form name="search" v-if="home">
    <label> Search Properties</label><br />
    <div class="group">
      <label class="form-label" for="Address">Address</label> <br />
      <input type="text" id = "Address" v-model="searchAddress" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="Apt">Apt</label> <br />
      <input class="form-field" name="Apt" id="Apt" v-model="searchApt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="yr_built">Year Built</label> <br />
      <input class="form-field" name="yr_built" id="yr_built" v-model="searchYearBuilt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="long">Longitude</label> <br />
      <input class="form-field" name="long" id="long" v-model="searchLong" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lat">Latitude</label> <br />
      <input class="form-field" name="lat" id="lat" v-model="searchLat" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="nbhd">Neighborhood</label> <br />
      <input class="form-field" name="nbhd" id="nbhd" v-model="searchNbhd" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="block">Block</label> <br />
      <input class="form-field" name="block" id="block" v-model="searchBlock" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lot">Lot</label> <br />
      <input class="form-field" name="lot" id="lot" v-model="searchLot" lazy>  
    </div>
    <div class="group">
      <label class="form-label" for="bldgcls">Building Class</label> <br />
    <input class="form-field" name="bldgcls" id="bldgcls" v-model="searchBldgCls" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="taxcls">Tax Class</label> <br />
    <input class="form-field" name="taxcls" id="taxcls" v-model="searchTaxCls" lazy>
    </div>
    <button type="submit" @click="searchProperties()"> Search </button>
  </form>
  <table border=1 v-if="home">
    <caption>Properties</caption>
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
        <td>{{ property.longitude }}</td>
        <td>{{ property.lat }}</td>
        <td>{{ property.nbhd }}</td>
        <td>{{ property.pblock }}</td>
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


  <table border=1 v-if="filteredpropertiesview">
    <caption>Properties</caption>
    <tr>
      <th colspan="10">Results</th>
    </tr>
    <tr>
      <th colspan="10">Searching For</th>
    </tr>
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
    <tr>
      <th>{{searchAddress}}</th>
      <th>{{searchApt}}</th>
      <th>{{searchYearBuilt}}</th>
      <th>{{searchLong}}</th>
      <th>{{searchLat}}</th>
      <th>{{searchNbhd}}</th>
      <th>{{searchBlock}}</th>
      <th>{{searchLot}}</th>
      <th>{{searchBldgCls}}</th>
      <th>{{searchTaxCls}}</th>
    </tr>
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
    <tr v-for="property in fproperties" v-bind:key="property" v-on:click="findsales(item)">
        <td>{{ property.address }}</td>
        <td>{{ property.apt }}</td>
        <td>{{ property.yr_built }}</td>
        <td>{{ property.longitude }}</td>
        <td>{{ property.lat }}</td>
        <td>{{ property.nbhd }}</td>
        <td>{{ property.pblock }}</td>
        <td>{{ property.lot }}</td>
        <td>{{ property.bldg_cls_p }}</td>
        <td>{{ property.tax_cls_p }}</td>
    </tr>
  </table>


  <table border=1 v-if="propertyview">
    <tr>
        <th>Building ID</th>
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
    <tr>
      <td> {{propertybbl}} </td>
      <td> {{propertyadd}} </td>
      <td> {{propertyapt}} </td>
      <td> {{propertyyrbuilt}} </td>
      <td> {{propertylong}} </td>
      <td> {{propertylat}} </td>
      <td> {{propertyngbd}} </td>
      <td> {{propertyblock}} </td>
      <td> {{propertylot}} </td>
      <td> {{propertybldgcls}} </td>
      <td> {{propertytaxcls}} </td>
    </tr>
    <tr>
      <td v-on:click="propertyview=false; home=true"><p>&#60;--Back</p></td>    
    </tr>
  </table>
  <table v-if="propertyview">
    <tr>
      <td>Sale Year</td>
      <td>Sale Easement</td>
      <td>Tax Class at Sale</td>
      <td>Building Class at Sale</td>
      <td>Sale Date</td>
      <td>Sale Price</td>
      <td>Resedential Units at Time of Sale</td>
      <td>Commerical Units at Time of Sale</td>
      <td>Total Units at Time of Sale</td>
      <td>Building Category at Time of Sale</td>
      <td>Notes on Sale</td>
    </tr>
    <tr v-for="sale in sales" v-bind:key="sale">
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
      fproperties: [],
      sales:[],
      count:0,
      filteredcount:0,
      nxt:"",
      fnxt:"",
      prev:"",
      fprev:"",
      start:0,
      fstart:0,
      end:0,
      fend:0,
      home:true,
      propertyview:false,
      filteredpropertiesview:false,
      property: "",
      propertybbl: "",
      propertyadd: "",
      propertyapt:"",
      propertyyrbuilt:"",
      propertylong:"",
      propertylat:"",
      propertyngbd:"",
      propertyblock:"",
      propertylot:"",
      propertybldgcls:"",
      propertytaxcls: "",
      searchAddress: null,
      searchApt: null,
      searchYearBuilt: null,
      searchLong: null,
      searchLat: null,
      searchNbhd: null,
      searchBlock: null,
      searchLot: null,
      searchBldgCls: null,
      searchTaxCls: null
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
    searchProperties: function(){
      this.home = false
      this.filteredpropertiesview = true
      let url='filterProperties'
      
      axios.get(encodeURI(url),{params:{
        address:this.searchAddress,
        apt:this.searchApt,
        yr_built:this.searchYearBuilt,
        longitude:this.searchLong,
        lat:this.searchLat,
        nbhd:this.searchNbhd,
        pblock:this.searchBlock,
        lot:this.searchLot,
        bldg_cls_p:this.searchBldgCls,
        tax_cls_p:this.searchTaxCls}}).then(resp =>{
        console.log(resp.data)
        this.fproperties = resp.data
      })
    },

    findsales: function (property) {
        this.home=false
        this.filteredpropertiesview = false
        this.propertyview=true
        this.property = property
        this.propertybbl = property.bbl_id
        this.propertyadd = property.address
        this.propertyapt = property.apt
        this.propertyyrbuilt = property.yr_built
        this.propertylong = property.longitude
        this.propertylat = property.lat
        this.propertyngbd = property.nbhd
        this.propertyblock = property.pblock
        this.propertylot = property.lot
        this.propertybldgcls = property.bldg_cls_p
        this.propertytaxcls = property.tax_cls_p

        

        let url='salesforproperty/?bbl_id='+property.bbl_id+'&address='+property.address+'&apt='+property.apt
        this.get(encodeURI(url)).then(response => {
            console.log(response)
            this.sales= response.data.results
            
        })
        console.log(this.sales)
    },

  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.group{
  display: inline-block;
}
form{
  margin-top: 5%;
  vertical-align: middle;
  margin-left: auto;
  margin-right:auto;
  text-align:center;
}
table{
  margin-top: 5%;
  vertical-align: middle;
  margin-left: auto;
  margin-right: auto;
  background-color: white;
  text-align: center;
}
</style>
