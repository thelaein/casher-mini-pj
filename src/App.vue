<template>
  <div class="container">
    <div class="row my-3">
      <div class="col-lg-8">
        <table class="table table-bordered table-striped table-primary">
          <thead>
          <tr>
            <th>#</th>
            <th>Name</th>
            <th>Unit</th>
            <th>Unit-Price</th>
            <th>Quantity</th>
            <th>Cost</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="record in records" class="animate__animated animate__fadeInDown" :key="record.id">
            <td>
              <span>{{record.id}}</span>
              <i @click="del(record.id)" class="fa-solid fa-trash text-danger"></i>
            </td>
            <td>{{record.product.name}}</td>
            <td>{{record.unit.name}}</td>
            <td>{{record.unit.price}}ကျပ်</td>
            <td>{{record.quantity}}</td>
            <td>{{record.cost}}</td>
          </tr>
          </tbody>
          <tfoot>
          <tr v-if="records.length > 0">
            <td colspan="5">Total</td>
            <td>{{records.reduce((up,c)=>up+c.cost,0)}}</td>
          </tr>
          </tfoot>
        </table>
      </div>
      <div class="col-lg-4">
        <div class="card">
          <div class="card-body">
            <h3 class="card-title mb-3">ကုန်ပစ်စည်း</h3>
            <form action="" @submit.prevent="saveRecord">
              <div class="my-3">
                <select class="form-select mb-3" v-model="selectedProduct" id="">
                  <option value="">Selected Product</option>
                  <option v-for="product in products" :value="product.id" :key="product.id">
                    {{product.name}}
                  </option>
                </select>
                <!--                <div>-->
                <!--                  <select class="form-select" v-model="selectedUnit">-->
                <!--                    <option v-if="selectedProduct === 0">Select Unit</option>-->
                <!--                    <option v-else="selectedProduct >0" v-for="unit in selectedProductDetail.unit" :key="unit.id" >-->
                <!--                      {{unit.name}}-->
                <!--                    </option>-->

                <!--                  </select>-->
                <!--                </div>-->
                <div v-if="selectedProduct >0">
                  <select class="form-select mb-3" v-model="selectedUnit" id="">
                    <option value="">Select Unit</option>
                    <option v-for="unit in selectedProduct>0 && selectedProductDetail.unit" :value="unit.id">
                      {{unit.name}} - [{{unit.price}}ကျပ်]
                    </option>
                  </select>
                </div>
                <!--                <div v-else>-->
                <!--                  <select class="form-select mb-3" id="">-->
                <!--                    <option value="">Select Unit</option>-->
                <!--                  </select>-->
                <!--                </div>-->

                <div class="mb-3">
                  <input type="number" placeholder="quantity" class="form-control" v-model="inputQuantity">
                </div>
              </div>
              <div class="" @click="saveRecord">
                <button class="btn btn-primary">Add</button>
              </div>

            </form>
<!--            {{records}}-->
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
      selectedProduct:"",
      selectedUnit:"",
      inputQuantity:null,
      recordStart:1,
      products: [
        {
          id:1,
          name:"apple",
          unit:[
            {
              id:1,
              name:"လုံး",
              price:110
            },
            {
              id:2,
              name:"ထုပ်",
              price:1000
            },
          ]
        },
        {
          id:2,
          name:"egg",
          unit:[
            {
              id:1,
              name:"လုံး",
              price:150
            },
            {
              id:2,
              name:"ကဒ်",
              price:1200
            },
          ]
        },
        {
          id:3,
          name:"ice-cream",
          unit:[
            {
              id:1,
              name:"ခွက်-ေသး",
              price:500
            },
            {
              id:2,
              name:"ခွက်-ကြီး",
              price:1000
            },
          ]
        },
        {
          id:4,
          name:"cheese-ball",
          unit:[
            {
              id:1,
              name:"ထုပ်-ေသး",
              price:700
            },
            {
              id:2,
              name:"ထုပ်-ကြီး",
              price:14000
            },
          ]
        },
        {
          id:5,
          name:"ခေါက်ဆွဲ",
          unit:[
            {
              id:1,
              name:"ထုပ်",
              price:500
            },
            {
              id:2,
              name:"ဒါဇင်",
              price:4000
            }
          ]
        },
      ],
      records:[],
    }
  },
  computed: {
    selectedProductDetail() {
      if (this.selectedProduct === null){
        return {}
      }
      return this.products.find(el=>el.id === this.selectedProduct)
    }
  },
  methods: {

    saveRecord() {
      let currentUnit=this.selectedProductDetail.unit.find(el=>el.id === this.selectedUnit)
      let record={
        id:this.recordStart,
        product:this.selectedProductDetail,
        unit:currentUnit,
        quantity:this.inputQuantity,
        cost:currentUnit.price * this.inputQuantity
      };
      //this.records.push(record);
      this.records=[...this.records,record]
      console.log(record);

      this.selectedProduct=this.selectedUnit=this.inputQuantity=""
      this.recordStart++

      // console.log(this.selectedProductDetail,this.selectedProduct,this.selectedUnit,this.inputQuantity)
    },
    del(recordId){
      this.records = this.records.filter(record => record.id != recordId)
      console.log(recordId)
    }
  },
}
</script>

<style lang="scss">

$primary : #6a4c93;
@import "~bootstrap/scss/bootstrap";
@import "~@fortawesome/fontawesome-free";
@import "~animate.css/animate.min.css";
</style>