<template>
    <div id="app">
        <div class="container">
            <h1 class="mb-5">Check out your BearthDay!</h1>
            <h4  v-if="showPicture">{{ pictureDate }}</h4>
            <p v-if="showPicture && isBdayMatch"> B<b>earth</b>Day!</p>
            <img class="earth-pic"  v-if="showPicture" :src="imageSrc"/>
            <div class="row justify-content-center align-items-center mt-5">
                <form class="form-inline" v-on:submit.prevent="getEarthPic">
                    <div class="form-group mr-3">
                        <input class="form-control" type="date" value="2018-02-12" id="bearthDay" v-model="birthday">
                    </div>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import moment from 'moment';

    export default {
        name: 'app',
        components: {},
        data() {
            return {
                birthday: null,
                showPicture: false,
                imageSrc: '',
                pictureDate: '',
                isBdayMatch: false,
                /**
                 * The DSCOVR satellite went offline and into "safe mode" after this date,
                 * no more pictures of Earth have been taken since then.
                 * See: https://spacenews.com/software-fix-planned-to-restore-dscovr/
                 */
                safeModeDate: moment('2019-06-27'),
            }
        },
        methods: {
            /**
             * Gets called when bday form is submitted
             */
            getEarthPic() {
                this.showPicture = false;
                this.isBdayMatch = false;
                let thisYearsBday = moment(moment(this.birthday).format('MM-DD-') + this.safeModeDate.format('YY'));
                //We can't use today's date to find a user's last bday since DSCOVR is offline so we use the safeModeDate
                let isPastSafeMode = thisYearsBday > this.safeModeDate;
                let lastBirthday = isPastSafeMode ? thisYearsBday.subtract(1, 'years') : thisYearsBday;
                this.makeNasaCall(lastBirthday);
            },
            /**
             * Makes call to the EPIC NASA api to retrieve an image of Earth for the given date
             * @param date
             */
            makeNasaCall(date) {
                const self = this;
                this.pictureDate = date.format('MM-DD-YYYY');
                axios({
                    method: 'GET',
                    url: `https://api.nasa.gov/EPIC/api/natural/date/${date.format('YYYY-MM-DD')}?api_key=0qwRJqJQSpLSijgFQyERlWyyhud6y0SwZtgcUOtO`
                }).then(function (response) {
                    //If there's data for the given date we want to render the picture of Earth.
                    if (response.data.length){
                        self.showPicture = true;
                        let image = response.data[0].image;
                        self.imageSrc = `https://api.nasa.gov/EPIC/archive/natural/${date.format('YYYY/MM/DD')}` + `/png/${image}.png?api_key=0qwRJqJQSpLSijgFQyERlWyyhud6y0SwZtgcUOtO`;
                    }
                    //Otherwise, increment the day and try again.
                    else {
                        self.isBdayMatch = false;
                        self.makeNasaCall(date.add(1, 'days'));
                    }
                })
                .catch(function (error) {
                    console.log(error);
                });
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
    .earth-pic {
        width: 300px;
    }
</style>
