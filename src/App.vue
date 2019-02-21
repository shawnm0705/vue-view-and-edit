<template>
  <div id="app">
    <view-and-edit
      width="100px"
      value="no value"
      v-on:save="onSave($event)"/>
  </div>
</template>

<script>
import ViewAndEdit from './components/ViewAndEdit.vue'

export default {
  name: 'app',
  components: {
    ViewAndEdit
  },
  methods: {
    onSave(value) {
      console.log(value)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
