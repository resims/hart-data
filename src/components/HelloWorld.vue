<template><body>
  <div v-if="home" class="header">
    <div class="header-img">
    </div>
  </div>   
  
  <form name="search" v-if="home">

    <label>Search By:</label>
    <select name="searchOption" v-model="searchOption" @change="onChange($event)">      
      <option value="Properties">All Properties</option>
      <option value="Borough">Borough</option>
    </select><br />
    
    <label> Search Properties</label><br />
    <div class="group">
      <label class="form-label" for="Address">Address</label> <br />
      <input type="text" placeholder="Address" id = "Address" v-model="searchAddress" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="Apt">Apt</label> <br />
      <input type="text" placeholder="Apartment #" class="form-field" name="Apt" id="Apt" v-model="searchApt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="yr_built">Year Built</label> <br />
      <input type="text" placeholder="Year Built" class="form-field" name="yr_built" id="yr_built" v-model="searchYearBuilt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="long">Longitude</label> <br />
      <input type="text" placeholder="Longitude" class="form-field" name="long" id="long" v-model="searchLong" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lat">Latitude</label> <br />
      <input type="text" placeholder="Latitude" class="form-field" name="lat" id="lat" v-model="searchLat" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="nbhd">Neighborhood</label> <br />
      <input type="text" placeholder="Neighborhood" class="form-field" name="nbhd" id="nbhd" v-model="searchNbhd" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="block">Block</label> <br />
      <input type="text" placeholder="Block" class="form-field" name="block" id="block" v-model="searchBlock" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lot">Lot</label> <br />
      <input type="text" placeholder="Lot" class="form-field" name="lot" id="lot" v-model="searchLot" lazy>  
    </div>
    <div class="group">
      <label class="form-label" for="bldgcls">Building Class</label> <br />
    <input type="text" placeholder="Building Class" class="form-field" name="bldgcls" id="bldgcls" v-model="searchBldgCls" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="taxcls">Tax Class</label> <br />
    <input type="text" placeholder="Tax Class" class="form-field" name="taxcls" id="taxcls" v-model="searchTaxCls" lazy>
    </div>
    <div class="group" v-if="searchBoroughView">
      <label class="form-label" for="searchBorough">Borough</label> <br />
      <select name="searchBorough" @change="onChangeBorough($event)" v-model="searchBorough">
        <option value="1">Manhattan</option>
        <option value="2">Bronx</option>
        <option value="3">Brooklyn</option>
        <option value="4">Queens</option>
        <option value="5">Staten Island</option>
      </select>
    </div>
    <button type="submit" @click="search()"> Search </button>
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

  <form name="addProperty" v-if="home">
    <label> Add Property</label><br />
    <div class="group">
      <label class="form-label" for="bID">Building ID</label><br />
      <input type="text" placeholder="Building ID" id="bID" v-model="newbbl_id" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="Address">Address</label> <br />
      <input type="text" placeholder="Address" id = "Address" v-model="newAddress" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="Apt">Apt</label> <br />
      <input type="text" placeholder="Apartment #" class="form-field" name="Apt" id="Apt" v-model="newApt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="yr_built">Year Built</label> <br />
      <input type="text" placeholder="Year Built" class="form-field" name="yr_built" id="yr_built" v-model="newYearBuilt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="long">Longitude</label> <br />
      <input type="text" placeholder="Longitude" class="form-field" name="long" id="long" v-model="newLong" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lat">Latitude</label> <br />
      <input type="text" placeholder="Latitude" class="form-field" name="lat" id="lat" v-model="newLat" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="nbhd">Neighborhood</label> <br />
      <input type="text" placeholder="Neighborhood" vclass="form-field" name="nbhd" id="nbhd" v-model="newNbhd" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="block">Block</label> <br />
      <input type="text" placeholder="Block" class="form-field" name="block" id="block" v-model="newBlock" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lot">Lot</label> <br />
      <input type="text" placeholder="Lot" class="form-field" name="lot" id="lot" v-model="newLot" lazy>  
    </div>
    <div class="group">
      <label class="form-label" for="bldgcls">Building Class</label> <br />
    <input type="text" placeholder="Building Class" class="form-field" name="bldgcls" id="bldgcls" v-model="newBldgCls" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="taxcls">Tax Class</label> <br />
    <input type="text" placeholder="Tax Class" class="form-field" name="taxcls" id="taxcls" v-model="newTaxCls" lazy>
    </div>
    <button type="button" @click="insertProperty()"> Add </button>
  </form>



  <table border=1 v-if="filteredpropertiesview">
    <caption>Properties</caption>

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
      <th colspan="10">Results</th>
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
    <tr v-for="property in fproperties" v-bind:key="property" v-on:click="findsales(property)">
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
    <caption>Property</caption>
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
        <th></th>
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
      <td v-on:click="removeProperty(propertybbl)">Remove</td>
    </tr>
    <tr>
      <td v-on:click="propertyview=false; home=true"><p>&#60;--Back</p></td>    
    </tr>
  </table>
  
  <form name="updateProperty" v-if="propertyview">
    <label> Update Property</label><br />
    <div class="group">
      <label class="form-label" for="Address">Address</label> <br />
      <input type="text" placeholder="Address" id = "Address" v-model="updatePropertyadd" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="Apt">Apt</label> <br />
      <input type="text" placeholder="Apartment #" class="form-field" name="Apt" id="Apt" v-model="updatePropertyapt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="yr_built">Year Built</label> <br />
      <input type="text" placeholder="Year Built" class="form-field" name="yr_built" id="yr_built" v-model="updatePropertyyrbuilt" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="long">Longitude</label> <br />
      <input type="text" placeholder="Longitude" class="form-field" name="long" id="long" v-model="updatePropertylong" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lat">Latitude</label> <br />
      <input type="text" placeholder="Latitude" class="form-field" name="lat" id="lat" v-model="updatePropertylat" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="nbhd">Neighborhood</label> <br />
      <input type="text" placeholder="Neighborhood" vclass="form-field" name="nbhd" id="nbhd" v-model="updatePropertynbhd" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="block">Block</label> <br />
      <input type="text" placeholder="Block" class="form-field" name="block" id="block" v-model="updatePropertyblock" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="lot">Lot</label> <br />
      <input type="text" placeholder="Lot" class="form-field" name="lot" id="lot" v-model="updatePropertylot" lazy>  
    </div>
    <div class="group">
      <label class="form-label" for="bldgcls">Building Class</label> <br />
    <input type="text" placeholder="Building Class" class="form-field" name="bldgcls" id="bldgcls" v-model="updatePropertybldgcls" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="taxcls">Tax Class</label> <br />
    <input type="text" placeholder="Tax Class" class="form-field" name="taxcls" id="taxcls" v-model="updatePropertytaxcls" lazy>
    </div>
    <button type="button" @click="updateProperty()"> Update </button>
  </form>
  <table border=1 v-if="propertyview">
    <caption>Sales</caption>
    <tr>
      <td>Sale ID</td>
      <td>Sale Year</td>
      <td>Zip Code</td>
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
      <td colspan="2"></td>      
    </tr>
    <tr v-for="sale in sales" v-bind:key="sale">
        <td>{{ sale.sale_id }} </td>
        <td>{{ sale.year }}</td>
        <td>{{sale.zip}}</td>
        <td>{{ sale.easmnt }}</td>
        <td>{{ sale.tax_cls_s }}</td>
        <td>{{ sale.bldg_cls_s }}</td>
        <td>{{ sale.sale_date }}</td>
        <td>{{ sale.price }}</td>
        <td>{{ sale.res_unit }}</td>
        <td>{{ sale.com_unit }}</td>
        <td>{{ sale.tot_unit }}</td>
        <td>{{ sale.bldg_ctgy }}</td>
        <td>{{ sale.message }}</td>
        <td v-on:click="openModal('update', sale)">Update</td>
        <td v-on:click="removeSale(sale)">Remove</td>
    </tr>
  </table>

  <table border=1 v-if="propertyview">
    <caption>Sales Statistics for Similar Properties</caption>
    <tr>
      <td>Minimum</td>
      <td>Average</td>
      <td>Maximum</td>
    </tr>
    <tr>
      <td>{{min}}</td>
      <td>{{avg}}</td>
      <td>{{max}}</td>
    </tr>
  </table>

   <form name="addSale" v-if="propertyview">
    <label> Add Sale</label><br />
    <div class="group">
      <label class="form-label" for="zip">Zip Code</label><br />
      <input type="text" placeholder="enter a 6 digit zip code" id="zip" v-model="newZip" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="year">Sale Year</label><br />
      <input type="text" placeholder="enter a 4 digit year" id="year" v-model="newSaleYear" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="easmnt">Easment</label> <br />
      <input type="text" placeholder="enter easment" id = "Address" v-model="newSaleEasmnt" lazy>
    </div>
        <div class="group">
      <label class="form-label" for="tax_cls_s">Tax Class during Sale</label> <br />
      <input type="text" placeholder="enter tax class" id = "tax_cls_s" v-model="newTax_cls_s" lazy>
    </div>
        <div class="group">
      <label class="form-label" for="bldg_cls_s">Building Class during Sale</label> <br />
      <input type="text" placeholder="enter building class" id = "Address" v-model="newBldg_cls_s" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="saledate">Sale Date</label> <br />
      <input type="text" placeholder="YYYY-MM-DD" id = "saledate" v-model="newSaleDate" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="saleprice">Sale Price</label> <br />
      <input type="text" placeholder="enter price #" id = "saleprice" v-model="newSalePrice" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="res_unit">Resedential Units</label> <br />
      <input type="text" placeholder="enter # of resedential units" id = "res_unit" v-model="newRes_unit" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="com_unit">Commercial Units</label> <br />
      <input type="text" placeholder="enter # of commercial units" id = "com_unit" v-model="newCom_unit" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="tot_unit">Total Units</label> <br />
      <input type="text" placeholder="enter total # of units" id = "tot_unit" v-model="newTot_unit" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="bldg_ctgy_s">Building Category</label> <br />
      <input type="text" placeholder="enter building category" id = "bldg_ctgy_s" v-model="newBldg_ctgy_s" lazy>
    </div>
    <div class="group">
      <label class="form-label" for="notes">Notes</label> <br />
      <input type="text" placeholder="enter notes" id = "notes" v-model="newNotes" lazy>
    </div>
    <button type="button" @click="insertSale()"> Add </button>
  </form>

  <div v-if="showModal">
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            Add the sale
          </div>
          <div class="modal-body">
              <table border=1>
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
                <tr>
                  <td>                    
                    <input type="hidden" class="form-field" name="bbl_id" v-model="updateSale_bbl_id" lazy>
                    <input type="text" class="form-field" name="year" v-model="updateSale_year" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="easmnt" v-model="updateSale_easmnt" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="tax_cls_s"  v-model="updateSale_tax_cls_s" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="bldg_cls_p" v-model="updateSale_bldg_cls_s" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="sale_date" v-model="updateSale_sale_date" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="price" v-model="updateSale_price" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="res_unit" v-model="updateSale_res_unit" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="com_unit" v-model="updateSale_com_unit" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="tot_unit" v-model="updateSale_tot_unit" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="bldg_ctgy" v-model="updateSale_bldg_ctgy" lazy>
                  </td>
                  <td>
                    <input type="text" class="form-field" name="message" v-model="updateSale_message" lazy>
                  </td>
                </tr>
              </table>
          </div>
          <div class="modal-footer">
            <button class="modal-default-button" v-on:click="updateSale(type)">{{type}}</button>
            <button class="modal-default-button" v-on:click="closeModal">Close</button>
          </div>
        </div>
      </div>
    </div>
  </transition>
  </div>

  <div v-if="propertyview">
    <h1>
      This property is located in {{boroughname}}
    </h1>
    <p>
      {{boroughdescription}}<br/>
    </p>
    <p v-if="boroughpopulation != null">
      {{boroughname}}'s Population Through the Decades:<br/>            
      <BarChart :boroughpopulation="boroughpopulation" :type="'first'"/> 

      {{boroughname}}'s % of NYC's Total Population Through the Decades:<br/>
      <BarChart :boroughpopulation="boroughpopulation" :type="'second'"/> 

    </p>
  </div>
  </body>
</template>

<script>
import axios from 'axios'
import BarChart from './BarChart.vue'
axios.defaults.baseURL = '//68.54.138.144:8080/';
export default {
  name: 'HelloWorld',  
  components: {
    BarChart
  },
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
      propertynbhd:"",
      propertyblock:"",
      propertylot:"",
      propertybldgcls:"",
      propertytaxcls: "",
      propertyborough: "",
      boroughname: "",
      boroughdescription: "",
      boroughpopulation: null,

      searchOption: "Properties",      
      searchBoroughView: false,

      searchAddress: null,
      searchApt: null,
      searchYearBuilt: null,
      searchLong: null,
      searchLat: null,
      searchNbhd: null,
      searchBlock: null,
      searchLot: null,
      searchBldgCls: null,
      searchTaxCls: null,
      searchBorough: "1",      

      newbbl_id: null,
      newAddress: null,
      newApt: null,
      newYearBuilt: null,
      newLong: null,
      newLat: null,
      newNbhd: null,
      newBlock: null,
      newLot: null,
      newBldgCls: null,
      newTaxCls: null,
      newZip: null,
      newSaleYear: null,
      newSaleEasmnt: null,
      newTax_cls_s: null,
      newBldg_cls_s: null,
      newSaleDate: null,
      newSalePrice: null,
      newRes_unit: null,
      newCom_unit: null,
      newTot_unit: null,
      newBldg_ctgy_s: null,
      newNotes: null,
      type: '',
      showModal: false,
      saleId: '',
      updateSale_bbl_id: '',
      updateSale_bldg_cls_s: '',
      updateSale_bldg_ctgy: '',
      updateSale_com_unit: '',
      updateSale_easmnt: '',
      updateSale_message: '',
      updateSale_price: '',
      updateSale_res_unit: '',
      updateSale_sale_date: '',
      updateSale_tax_cls_s: '',
      updateSale_tot_unit: '',
      updateSale_url: '',
      updateSale_year: '',
      updateSale_zip: '',
      updatePropertyadd: "",
      updatePropertyapt:"",
      updatePropertyyrbuilt:"",
      updatePropertylong:"",
      updatePropertylat:"",
      updatePropertynbhd:"",
      updatePropertyblock:"",
      updatePropertylot:"",
      updatePropertybldgcls:"",
      updatePropertytaxcls: "",

      max: 0,
      min: 0,
      avg: 0
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

    onChange: function(event) {
      console.log("search option", event.target.value)
      let viewOption = event.target.value
      if(viewOption == "Properties") {        
        this.searchBoroughView = false
      }
      if(viewOption == "Borough") {
        this.searchBoroughView = true        
      }
    },
    onChangeBorough: function(event) {
      this.searchBorough = event.target.value
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
            if(response.data.next!== null){
              this.nxt = response.data.next.split("?")[1]
            }
            if(response.data.previous !== null){
              this.prev=response.data.previous.split("?")[1]
            }
            if(response.data.previous == null && response.data.next !== null){
              this.start=1
              this.end = 10
            }
            if(response.data.previous.split("?")[1] == null){
              this.start = 11
              this.end = 20
            }
            else{
              this.start=1+this.properties.length*parseInt(this.prev.split("=")[1])
              this.end = this.start+9
            }
        })
        console.log(this.nxt)
    },
    search: function(){
      this.home = false
      if(this.searchBoroughView == false) {
        // Search Properties
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
      } else {
        // Search Borough
        let url = "PropertyForBorough"
        axios.get(encodeURI(url),{params:{
          searchborough: this.searchBorough,
          address:this.searchAddress,
          apt:this.searchApt,
          yr_built:this.searchYearBuilt,
          longitude:this.searchLong,
          lat:this.searchLat,
          nbhd:this.searchNbhd,
          pblock:this.searchBlock,
          lot:this.searchLot,
          bldg_cls_p:this.searchBldgCls,
          tax_cls_p:this.searchTaxCls}}).then(response => {
            console.log("response borough", response, this.searchBorough)
          this.fproperties = response.data
        })
      }
    },
    findsales: async function (property) {
      console.log("property", property)
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

        let boroughurl = 'getBorough/?nbhd='+this.propertyngbd
        await this.get(encodeURI(boroughurl)).then(response => {
          console.log("borough", response)
          this.propertyborough = response.data.results[0]
          this.propertyboroughcode = this.propertyborough.borough
          console.log("borough", this.propertyborough, this.propertyboroughcode)
        })

        let endpoint = 'http://68.54.138.144:8080/propertydescriptiondetail/'+this.propertyboroughcode
        await axios.get(endpoint).then(response => {
          console.log("response data", response)
          this.boroughdescription = response.data.description
          this.boroughname = response.data.borough
          this.boroughpopulation = JSON.parse(response.data.population.replace(/'/g,'"'))
          console.log("boroughname",this.boroughname)
          console.log("boroughPopulation",this.boroughpopulation, typeof this.boroughpopulation)          
        })

        // for update property
        this.updatePropertyadd = property.address
        this.updatePropertyapt = property.apt
        this.updatePropertyyrbuilt = property.yr_built
        this.updatePropertylong = property.longitude
        this.updatePropertylat = property.lat
        this.updatePropertynbhd = property.nbhd
        this.updatePropertyblock = property.pblock
        this.updatePropertylot = property.lot
        this.updatePropertybldgcls = property.bldg_cls_p
        this.updatePropertytaxcls = property.tax_cls_p

        
        let url='salesforproperty/?search_bbl_id='+this.propertybbl
        await this.get(encodeURI(url)).then(response => {
            console.log("response", response)
            this.sales= response.data              
        })       

        let url_fors_tats = `/StatsForProperty/?search_nbhd=${this.propertyngbd}&search_bldg_cls_p=${this.propertybldgcls}&search_tax_cls_p=${this.propertytaxcls}`
        await this.get((encodeURI(url_fors_tats))).then((res) => {
          this.max = res.data[0].maximum
          this.min = res.data[0].minimum
          this.avg = res.data[0].average
          console.log("res", res)
        })
        
    },    
    updateSale: function(type) {
      if(type == 'update') {      
        const updateSale = {
          sale_id: this.saleId,
          bbl_id: this.updateSale_bbl_id,
          year: this.updateSale_year,
          easmnt: this.updateSale_easmnt,
          tax_cls_s: this.updateSale_tax_cls_s,
          bldg_cls_s: this.updateSale_bldg_cls_s,
          sale_date: this.updateSale_sale_date,
          price: this.updateSale_price,
          res_unit: this.updateSale_res_unit,
          com_unit: this.updateSale_com_unit,
          tot_unit: this.updateSale_tot_unit,
          bldg_ctgy: this.updateSale_bldg_ctgy,
          message: this.updateSale_message
        }
        let url = 'updateSale/' + this.saleId;
        console.log("update sale", updateSale, url, this.saleId);
        axios.put(url, updateSale).then(res => console.log("updateSale result", res))
      }
      if(type == 'insert') {
        const newSale = {         
          bbl_id: this.updateSale_bbl_id, 
          year: this.updateSale_year,
          easmnt: this.updateSale_easmnt,
          tax_cls_s: this.updateSale_tax_cls_s,
          bldg_cls_s: this.updateSale_bldg_cls_s,
          sale_date: this.updateSale_sale_date,
          price: this.updateSale_price,
          res_unit: this.updateSale_res_unit,
          com_unit: this.updateSale_com_unit,
          tot_unit: this.updateSale_tot_unit,
          bldg_ctgy: this.updateSale_bldg_ctgy,
          message: this.updateSale_message,
          zip: null
        }
        console.log("new Sale", newSale)
        let url = 'salesforproperty/'

        axios.post(url, newSale).then(res => console.log("inserted new sale", res))
      }
      let url='salesforproperty/?search_bbl_id='+this.propertybbl
          this.get(encodeURI(url)).then(response => {
              console.log("response", response)
              this.sales= response.data
              
          })

    },
    openModal: function(type, sale) {
      this.showModal = true      
      if(type == 'update') {
        this.saleId = sale.sale_id
        this.updateSale_bbl_id = sale.bbl_id
        this.updateSale_year =  sale.year
        this.updateSale_easmnt = sale.easmnt
        this.updateSale_tax_cls_s = sale.tax_cls_s
        this.updateSale_bldg_cls_s = sale.bldg_cls_s
        this.updateSale_sale_date = sale.sale_date      
        this.updateSale_price = sale.price
        this.updateSale_res_unit = sale.res_unit
        this.updateSale_com_unit = sale.com_unit
        this.updateSale_tot_unit = sale.tot_unit
        this.updateSale_bldg_ctgy = sale.bldg_ctgy
        this.updateSale_message = sale.message     
        this.type = type 
      } 
    },
    closeModal: function() {
      this.showModal = false
    },
    removeSale: function(sale) {
      let url = "deleteSale/" + sale.sale_id
      console.log("url", url)
      axios.delete(url).then(res => {
        console.log("response", res)
        location.reload()
      })
    },
    insertSale: function(){


      console.log("insertSale clicked!")   
      console.log(this.propertybbl, this.newZip)   

      axios.post('sales/',{
        bbl_id: this.propertybbl,
        sale_id: "000",
        zip: this.newZip,
        year: this.newSaleYear,
        easmnt: this.newSaleEasmnt,
        tax_cls_s: this.newTax_cls_s,
        bldg_cls_s: this.newBldg_cls_s,
        sale_date: this.newSaleDate,
        price: this.newSalePrice,
        res_unit: this.newRes_unit,
        com_unit: this.newCom_unit,
        tot_unit: this.newTot_unit,
        bldg_ctgy: this.newBldg_ctgy_s,
        message: this.newNotes}).then((response)=> {
          console.log("response", response)
          let url='salesforproperty/?search_bbl_id='+this.propertybbl
          this.get(encodeURI(url)).then(response => {
              console.log("response", response)
              this.sales= response.data
              
          })
        });

        this.newZip = null,
        this.newSaleYear = null,
        this.newSaleEasmnt = null,
        this.newTax_cls_s = null,
        this.newBldg_cls_s = null,
        this.newSaleDate = null,
        this.newSalePrice = null,
        this.newRes_unit = null,
        this.newCom_unit = null,
        this.newTot_unit = null,
        this.newBldg_ctgy_s = null,
        this.newNotes = null
    },
    insertProperty: function(){
      let url = 'properties/'

      console.log("insertProperty clicked!")      

      axios.post(url,{
        bbl_id: this.newbbl_id,
        address: this.newAddress,
        apt: this.newApt,
        yr_built: this.newYearBuilt,
        longitude: this.newLong,
        lat: this.newLat,
        nbhd: this.newNbhd,
        pblock: this.newBlock,
        lot: this.newLot,
        bldg_cls_p: this.newBldgCls,
        tax_cls_p: this.newTaxCls}).then((response)=> {console.log(response);});

        this.newbbl_id = null,
        this.newAddress = null,
        this.newApt = null,
        this.newYearBuilt = null,
        this.newLong = null,
        this.newLat = null,
        this.newNbhd = null,
        this.newBlock = null,
        this.newLot = null,
        this.newBldgCls = null,
        this.newTaxCls = null
    },
    removeProperty: function(bbl_id){      
      let url = "deleteProperty/" + bbl_id
      axios.delete(url).then(res => {
        console.log("response", res)
        location.reload()
      })
    },
    updateProperty: function(){
      console.log("updateProperty clicked!")
      const updateProperty ={
        bbl_id: this.propertybbl,
        address: this.updatePropertyadd,
        apt: this.updatePropertyapt,
        yr_built: this.updatePropertyyrbuilt,
        longitude: this.updatePropertylong,
        lat: this.updatePropertylat,
        nbhd: this.updatePropertynbhd,
        pblock: this.updatePropertyblock,
        lot: this.updatePropertylot,
        bldg_cls_p: this.updatePropertybldgcls,
        tax_cls_p: this.updatePropertytaxcls
      }      
      let url = 'updateProperty/'+this.propertybbl;
      console.log("update property", updateProperty);
      axios.put(url,updateProperty
      ).then(res => {
        let property = res.data
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
      })
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  padding: 5%;
  margin-left: auto;
  margin-right: auto;
  align: middle;
  text-align: center;
  background-color: #d7f4fa;
}
p{
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  background-color: #d7f4fa;
}
.header{
  height: 320px;
}
.header .header-img{
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
  background-color: #f5f5f5;
  height: 100%;
  background-image: url(https://www.nycctp.com/wp-content/uploads/2019/06/nycctp-website-hero-image-home.jpg);
}
.group{
  display: inline-block;
}
form{
  vertical-align: middle;
  margin-left: auto;
  margin-right:auto;
  text-align:center;
  box-sizing: border-box;
  background-color: rgba(41, 126, 75, 0.651);
  box-shadow: 0 0 15px 4px rgba(22, 21, 21, 0.06);
}
table{
  vertical-align: middle;
  margin-left: auto;
  margin-right: auto;
  background-color: white;
  text-align: center;
  margin-bottom: 5%;
  margin-top: 5%;
}
input[type=text]{
  padding: 10px;
  margin: 10px 0;
  box-shadow: 0 0 15px 4px rgba(71, 68, 68, 0.06);
  border-radius: 10px;
  width:100%;
}

.modal-mask {
  position: fixed;
  z-index: 9999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 100%;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}


</style>
