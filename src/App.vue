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
              <form action="">
                <select name="" id="" class="form-select" v-model="selectedProduct">
                  <option value="">Select Product</option>
                  <option v-for="product in products" :value="product.id" :key="product.id">{{product.name}}</option>
                </select>
                <div class="">
                  <select v-model="selectedUnit" class="form-select">
                    <option v-if="selectedProduct === 0 ">Select Unit</option>
                    <option v-for="unit in selectedProductDetail.unit" :key="unit.id" >
                      {{unit.name}}
                    </option>
                  </select>
                </div>

              </form>
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
      if (this.selectedProduct === ''){
        return {}
      }
      return this.products.find(el=>el.id === this.selectedProduct);
    }
  },
}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~@fortawesome/fontawesome-free/css/all.min.css";
</style>