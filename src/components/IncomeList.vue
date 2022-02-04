<template>
  <div class="income-list">
      <incomeItem v-for="obj in state.sortedIncome" :key="obj.id" :income="obj" @remove-item="removeItem"/>
  </div>
</template>

<script>
import incomeItem from './incomeItem.vue'
export default {
    name: 'incomeList',
    components: {
        incomeItem
    },
    props: {
        state: Object
    },
    setup(props, {emit}) {
        function removeItem(id){
            emit('remove-item', id)
        }
        return {
            incomeItem,
            removeItem
        }
    }
}
</script>

<style scoped>
    .income-list {
        margin-top: 30px;
        padding: 15px;
    }
</style>