<template xmlns="http://www.w3.org/1999/html">
  <div class="container">
<div class="row my-3">
  <div class="col-lg-8">
  <table class="table table-bordered table-hover">
    <thead>
    <tr>
      <th class="text-center">#</th>
      <th class="text-center">Name</th>
      <th class="text-center">Price</th>
      <th class="text-center">Unit</th>
      <th class="text-center">Qty</th>
      <th class="text-center">Cost</th>
    </tr>
    </thead>
    <tbody >
    <tr  v-for="record in records" :key="record.id">
      <td>{{record.id}}</td>
      <td class="text-center">{{record.product.name}}</td>
      <td class="text-end">{{record.unit.price}}</td>
      <td>{{record.unit.name}}</td>
      <td>{{record.quantity}}</td>
      <td class="text-end">{{record.cost}}</td>
    </tr>
    </tbody>
    <tr v-if="records.length === 0">
      <td class="text-center" colspan="6"> There is no data</td>
    </tr>
    <tfoot>
    <tr v-if="records.length > 0">
      <td class="text-center" colspan="5"> ALL TOTAL</td>
      <td class="text-end"> {{records.reduce((pv,cv)=>pv+cv.cost,0)}}</td>
    </tr>
    </tfoot>
  </table>
  </div>
  <div class="col-lg-4">
    <div class="card">
      <div class="card-body">
        <ht class="card-title"> Products</ht>
        <form ref="AppForm"  action="" @submit.prevent="saveRecord">
          <div class="my-2">
            <select  class="form-select" id="" v-model="selectProduct">
              <option value="">
                Select Product
              </option>
              <option v-for="(product,index) in products" :value="product.id" :key="index">{{product.name}}</option>
            </select>
          </div>
          <div v-if="selectProduct > 0">
            <select class="form-select" name="" id="" v-model="selectUnit">
              <option value="">
                Select Unit
              </option>
              <option v-for="(unit,index) in selectProduct>0 && selectedProductDetail.unit" :key="unit.id" :value="unit.id">
                {{unit.name}} - {{ [unit.price]}}
              </option>
            </select>
          </div>
          <div v-else class="">
            <select class="form-select" name="" id="">
              <option value="">
                Empty Unit
              </option>
            </select>
          </div>
          <div class="my-2">
            <input v-model="inputQty" class="form-control" type="number">
          </div>
          <button class="btn btn-primary">
            <i class="fa-solid fa-plus"></i>
          </button>
      </form>

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
      recordStart : 1,
      selectUnit:"",
      selectProduct:"",
      inputQty : null,
      products: [
        {
          id:1,
          name: "Apple",
          unit : [
            {
              id : 1,
              name : "လုံး",
              price : 600
            },
            {
              id : 2,
              name : "ဒါဇင်",
              price: 7000
            }
          ]
        },
        {
          id:2,
          name: "Xiaomi",
          unit : [
            {
              id : 1,
              name : "လုံး",
              price : 500
            },
            {
              id : 2,
              name : "ဒါဇင်",
              price: 5500
            }
          ]
        },
        {
          id:3,
          name: "OPPO",
          unit : [
            {
              id : 1,
              name : "လုံး",
              price : 400
            },
            {
              id : 2,
              name : "ဒါဇင်",
              price: 4500
            }
          ]
        },
        {
          id:4,
          name: "VIVO",
          unit : [
            {
              id : 1,
              name : "လုံး",
              price : 300
            },
            {
              id : 2,
              name : "ဒါဇင်",
              price: 3500
            }
          ]
        },
        {
          id:5,
          name: "HUAWEI",
          unit : [
            {
              id : 1,
              name : "လုံး",
              price : 200
            },
            {
              id : 2,
              name : "ဒါဇင်",
              price: 2300
            }
          ]
        },
        {
          id:6,
          name: "One Plus",
          unit : [
            {
              id : 1,
              name : "လုံး",
              price : 100
            },
            {
              id : 2,
              name : "ဒါဇင်",
              price: 800
            }
          ]
        }
      ],
      records : []
    }
  },
  computed: {
    selectedProductDetail() {
      if (this.selectProduct === null)
      {
        return {}
      }
return this.products.find(el=>el.id === this.selectProduct);
    },
    selectedUnitDetail(){
      return this.selectProduct.find(el=>el === this.selectUnit);
    }
  },
  methods: {
    saveRecord() {
      let currentUnit = this.selectedProductDetail.unit.find(el=>el.id === this.selectUnit)
      let record = {
        id : this.recordStart,
        product: this.selectedProductDetail,
        unit : currentUnit,
        quantity : this.inputQty,
        cost : currentUnit.price * this.inputQty
      }
      this.records = [
          ...this.records,record
      ]
      this.recordStart++
    }
  },
}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.min.css";
@import "~@fortawesome/fontawesome-free/css/all.min.css";
</style>