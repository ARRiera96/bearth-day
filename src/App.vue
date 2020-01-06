<template>
  <div id="app">
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
      <div class="form-group row">
          <h1>BearthDay</h1>
          <div class="col-10">
              <label for="example-date-input" class="col-2 col-form-label">Date</label>
              <input class="form-control ml-1" type="date" value="2011-08-19" id="example-date-input">
          </div>
      </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
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
