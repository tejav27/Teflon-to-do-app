<template>
  <div>
      <TodoItem v-for="item in todos" :key="item" :listItem="item" v-on:deleteEvent="deletethat"/>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
    components:{TodoItem},
    props:['todos', 'deletethat'],
    methods:{
       
    }
}
</script>

<style>

</style>