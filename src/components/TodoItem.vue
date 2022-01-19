<template>
  <div>
     <li>{{listItem.content}} <button @click="deleteItem">delete</button></li>
  </div>
</template>

<script>
export default {
 props:['listItem'],
 methods:{
     deleteItem(){
         this.$emit('deleteEvent',this.listItem.id)
     }
 }
}
</script>

<style>

</style>