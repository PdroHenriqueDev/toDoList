<template>
  <div id="app">
    <List id="list-component"/>
  </div>
</template>

<script>
import List from './components/List.vue'

export default {
  name: 'App',
  components: {
    List
  }
}
</script>

<style>
body{
  background: linear-gradient(-135deg, #c850c0, #4158d0);
  display: flex;
  justify-content: center;
  overflow: hidden;
}

</style>
