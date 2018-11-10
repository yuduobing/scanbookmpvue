<template>
  <div >

     <Todolist></Todolist>

  </div>
</template>

<script>
  /* eslint-disable no-unused-expressions */
  import Todolist from '@/components/Todolist'
  export default {
    components: {
      Todolist
    }
  }
</script>
<style>
  li.done {
    text-decoration: line-through;
    color: red;
  }
</style>
