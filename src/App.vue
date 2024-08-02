<script setup>
  import { ref } from 'vue';
  const products = ref([
    {
      id: 1,
      name:'珍珠奶茶',
      description:'香濃奶茶搭配QQ珍珠',
      price:50,
      stock:20
    },
    {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
    },
    {
      id: 3,
      name: '翡翠檸檬',
      description: '綠茶與檸檬的完美結合',
      price: 55,
      stock: 34
    },
    {
      id: 4,
      name: '四季春茶',
      description: '香醇四季春茶，回甘無比',
      price: 45,
      stock: 10
    },
    {
      id: 5,
      name: '阿薩姆奶茶',
      description: '阿薩姆紅茶搭配香醇鮮奶',
      price: 50,
      stock: 25
    },
    {
      id: 6,
      name: '檸檬冰茶',
      description: '檸檬與冰茶的清新組合',
      price: 45,
      stock: 20
    },
    {
      id: 7,
      name: '芒果綠茶',
      description: '芒果與綠茶的獨特風味',
      price: 55,
      stock: 18
    },
    {
      id: 8,
      name: '抹茶拿鐵',
      description: '抹茶與鮮奶的絕配',
      price: 60,
      stock: 20
    }
  ])
  const addStock = (item)=>{
    item.stock++
  } 
  const subtractStock = (item)=>{
    if (item.stock>0){
      item.stock--
    }
  }
  const editText = ref({
      id: '',
      name:'',
      description:'',
      price:'',
      stock:''
  })
  const editMode = (item)=>{
    editText.value ={...item}//編輯 > 拷貝原內容，使綁定值不連動
  }
  const comfirmEdit =()=>{
    const index = products.value.findIndex(item=> item.id === editText.value.id);//取出索引值
    products.value[index]=editText.value;//指定索引值覆蓋整個內容
    editText.value={};//清空編輯框
  }
</script>

<template>
  <h3>2024 Vue 前端新手營</h3>
  <h4>week 1</h4>
  <table>
    <thead>
    <tr>
      <th scope="col">品項</th>
      <th scope="col">描述</th>
      <th scope="col">價格</th>
      <th></th>
      <th scope="col">庫存</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(item) in products" v-bind:key="item.id">
    <td>{{item.name}}</td>
    <td><small>{{item.description}}</small></td>
    <td>{{item.price}}</td>
    <td><button type="button" @click="subtractStock(item)"> - </button></td>
    <td>
      {{ item.stock }}
    </td>
    <td><button type="button" @click="addStock(item)"> + </button></td>
    <td>
      <button type="button" @click="editMode(item)">編輯</button>
    </td>
    </tr>
  </tbody>
  </table>
  <!--if 編輯內容id存在(有被抓到) 確認及取消都會改為空值，所以會消失-->
  <div v-if="editText.id">
    <hr>
    <h3>編輯區域</h3>
    <label for="name">品項</label>
    <input id="name" type="text" v-model="editText.name">
    <br>
    <label for="description">描述</label>
    <input id="description" type="text" v-model="editText.description">
    <br>
    <label for="price">價格</label>
    <input id="price" type="number" v-model="editText.price">
    <br>
    <label for="stock">數量</label>
    <input id="stock" type="number" v-model="editText.stock">
    <br>
    <button type="button" @click="comfirmEdit">確認</button>
    <button type="button" @click="editText={}">取消</button>
  </div>
  
  
</template>
 
<style scoped>
th {
  border-bottom: 1px dashed #000000;
}
</style>
