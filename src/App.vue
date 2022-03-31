<template>
  <div class="container">
    <div class="row my-3">
      <div class="col-lg-8">

      </div>
      <div class="col-lg-4">
        <div class="card">
          <div class="card-body">
            <h3 class="card-title mb-3">ကုန်စည်း</h3>
            <div class="mb-3">
              <form action="" @submit.prevent="saveRecord">
                <select  class="form-select mb-3" v-model="selectedProduct">
                  <option value="">Select Product</option>
                  <option v-for="product in products" :value="product.id" :key="product.id">{{product.name}}</option>
                </select>
                <div class="mb-3" v-if="selectedProduct > 0">
<!--                  <div class="form-check" v-for="unit in selectedProductDetail.unit">-->
<!--                    <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1">-->
<!--                    <label class="form-check-label" for="flexRadioDefault1">-->
<!--                      {{unit.name}}[{{unit.price}}kyat]-->
<!--                    </label>-->
<!--                  </div>-->
                  <select v-model="selectedUnit" class="form-select mb-3">
                    <option value="">Select Unit</option>
                    <option v-for="unit in selectedProduct>0 && selectedProductDetail.unit" :value="unit.id" :key="unit.id" >
                      {{unit.name}} - [{{unit.price}}ကျပ်]
                    </option>
                  </select>
                </div>

<!--                <div v-else>-->
<!--                  <select class="form-select mb-3">-->
<!--                    <option value="">Select Unit</option>-->
<!--                  </select>-->
<!--                </div>-->

                <div class="mb-3">
                  <input  class="form-control" type="number" v-model="inputQuantity" placeholder="quantity">
                </div>
                <div class="" @click="saveRecord">
                  <button class="btn btn-primary">Add</button>
                </div>
              </form>
              {{records}}

            </div>

          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedProduct:'',
      selectedUnit:'',
      inputQuantity:null,
      records:[],
      products: [
        {
          id: 1,
          name:'Apple',
          unit:[
            {
              name:'လုံး',
              price:110
            },
            {
              name:'ထုပ်',
              price:1000
            },
          ]
        },
        {
          id: 2,
          name:'Egg',
          unit:[
            {
              name:'လုံး',
              price:160
            },
            {
              name:'ထုပ်',
              price:1500
            },
          ]
        },
        {
          id: 3,
          name:'Milk',
          unit:[
            {
              name:'ဘူး',
              price:1000
            },
            {
              name:'ကပ်',
              price:5000
            },
          ]
        },
        {
          id: 4,
          name:'cheeseball',
          unit:[
            {
              name:'လုံး',
              price:700
            },
            {
              name:'ထုပ်',
              price:10000
            },
          ]
        },
        {
          id: 5,
          name:'ice-cream',
          unit:[
            {
              name:'ဘူးေသး',
              price:500
            },
            {
              name:'ဘူးကြီး',
              price:2000
            },
          ]
        }

      ]
    }
  },
  computed: {
    selectedProductDetail() {
      if (this.selectedProduct === null){
        return {}
      }
      return this.products.find(el=>el.id === this.selectedProduct);
    }
  },
  methods: {
    saveRecord() {
      let currentUnit = this.selectedProductDetail.unit.find(el=>el.id === this.selectedUnit)
      let record = {
        product:this.selectedProductDetail,
        unit:currentUnit,
        quantity:this.inputQuantity,
        cost:currentUnit.price *this.inputQuantity
      }
      this.records=[...this.records,record]

      console.log(record);

      this.selectedProduct=this.selectedUnit=this.inputQuantity=''
    }
  },

}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~@fortawesome/fontawesome-free/css/all.min.css";
</style>