<template>
<div>
  <Header :totalIncome="state.totalIncome"/>
  <Form :state="state" @add-income="AddIncome"/>
  <incomeList :state="state" @remove-item="removeItem"/>
</div>
</template>

<script>
import { reactive, computed } from 'vue'
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import incomeList from './components/IncomeList.vue'
export default {
  name: 'App',
 components: {
   Header,
   Form,
   incomeList
 },
 setup() {
   const state = reactive ({
     income: [],

     totalIncome: computed(() => {
       let temp = 0;
       if (state.income.length>0) {
         for(let i = 0; i < state.income.length; i++){
           temp += state.income[i].value;
         }
         return temp;
       }else {
       return 0;
     }
    }),
     sortedIncome: computed(() => {
       let temp = [];

       temp = state.income.sort(function(a, b){
         return b.date - a.date;
       });

       return temp;
     })
   });

   function AddIncome(obj){
     let d = obj.date.split("-");
     let newD = new Date(d[0], d[1], d[2]);

     state.income = [...state.income, {
       id: Date.now(),
       desc: obj.desc,
       value: parseInt(obj.value),
       date: newD.getTime()
     }];
   } 

   function removeItem(id) {
     state.income = state.income.filter(v => v.id != id);
   }

   return {
     Header,
     state,
     AddIncome,
     incomeList,
     Form,
     removeItem
   }
 }
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background: #EEE;
}
</style>
