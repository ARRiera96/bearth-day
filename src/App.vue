<template>
    <div id="app">
        <!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
        <form v-on:submit.prevent="getImg">
            <div class="form-group">
                <h1>BearthDay</h1>
                <div class="col-3">
                    <label for="bearthDay" class="col-2 col-form-label">Date</label>
                    <input class="form-control" type="date" value="2018-02-12" id="bearthDay" v-model="birthday">
                </div>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>

        <img v-if="showPicture" :src="imageSrc"/>
    </div>
</template>

<script>
    // import HelloWorld from './components/HelloWorld.vue'
    // import axios from 'axios';
    import moment from 'moment';

    export default {
        name: 'app',
        components: {},
        data() {
            return {
                birthday: null,
                showPicture: false,
                imageSrc: '',
                safeModeDate: moment('2019-06-27')
            }
        },
        methods: {
            getImg() {
                //toggleTrigger
                this.showPicture = false;
                let lastBirthday = moment(this.birthday).format('MM-DD-') + this.safeModeDate.format('YY');
                let greater = moment(lastBirthday) > this.safeModeDate;
                let year = greater? this.safeModeDate.format('YYYY') - 1: this.safeModeDate.format('YYYY');
                this.epicNasaCall(year);
            },
            epicNasaCall() {
                // axios({
                //     method: 'GET',
                //     url: `https://api.nasa.gov/EPIC/api/natural/date/${this.birthday}?api_key=0qwRJqJQSpLSijgFQyERlWyyhud6y0SwZtgcUOtO`
                // }).then(function (response) {
                //     alert(JSON.stringify(response));
                //     if (response.data){
                //
                //     }
                //     else {
                //         this.epicNasaCall();
                //     }
                // })
                // .catch(function () {
                //     //handle error
                // });
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
