<template>
  <div id="app">
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
      <form v-on:submit.prevent="getImg">
          <div class="form-group">
              <h1>BearthDay</h1>
              <div class="col-3">
                  <label for="bearthDay" class="col-2 col-form-label">Date</label>
                  <input class="form-control" type="date" value="" id="bearthDay" v-model="birthday" >
              </div>
          </div>
          <button type="submit" class="btn btn-primary">Submit</button>
      </form>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
  },
    data() {
        return {
            birthday: null
        }
    },
    methods: {
        getImg(){
            alert(this.birthday);
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
