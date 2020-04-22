<template>
    <div>
        <apexchart width="500" type="line" :options="options" :series="series"></apexchart>
    </div>
</template>

<script>

    import moment from 'moment';
    import axios from 'axios';

    export default {
        name: "graphics",
        props: {
            date: Date,
            date2: Date,
            latitude: Number,
            longitude: Number
        },
        data: function() {
            return {
                dates: this.getDates(this.date, this.date2),
                options: {
                    chart: {
                        id: 'vuechart-example',
                        /*toolbar: {
                            show: false
                        },*/
                        zoom: {
                            type: 'x',
                            enabled: true,
                            autoScaleYaxis: true
                        },
                    },
                    xaxis: {
                        categories: this.getDates(this.date, this.date2)
                    }
                },
                series: [/*{
                    name: 'Tunnid',
                    data: this.getHours()
                },*/{
                    name: 'Minutid',
                    data: this.getMinutes()
                }/*,{
                    name: 'Sekundit',
                    data: this.getSeconds()
                }*/]
            }
        },
        methods: {
            getDates(startDate, stopDate) {
                // https://stackoverflow.com/questions/4413590/javascript-get-array-of-dates-between-2-dates
                var dateArray = [];
                var currentDate = moment(startDate);
                stopDate = moment(stopDate);
                while (currentDate <= stopDate) {
                    dateArray.push( moment(currentDate).format('YYYY-MM-DD') );
                    currentDate = moment(currentDate).add(1, 'days');
                }
                this.dates=dateArray;
                return dateArray;
            },
            getSeconds(){
                let latitude = this.latitude;
                let longitude = this.longitude;
                let sekundit = [];
                this.dates.forEach(function (date) {
                    axios.get('https://api.sunrise-sunset.org/json?lat='+latitude+'&lng='+longitude+'&'+date+'&formatted=0')
                        .then(response => {
                            sekundit.push(response.data['results']["day_length"])
                        })
                        .catch(e => {
                            alert(e);
                        })
                });
                this.dates=[];
                return sekundit;
            },
            getMinutes(){
                let latitude = this.latitude;
                let longitude = this.longitude;
                let minutid = [];
                this.dates.forEach(function (date) {
                    axios.get('https://api.sunrise-sunset.org/json?lat='+latitude+'&lng='+longitude+'&'+date+'&formatted=0')
                        .then(response => {
                            minutid.push(Math.round(response.data['results']["day_length"]/60*100)/100)
                        })
                        .catch(e => {
                            alert(e);
                        })
                });

                return minutid;
            },
            getHours(){
                let latitude = this.latitude;
                let longitude = this.longitude;
                let tunnid = [];
                this.dates.forEach(function (date) {
                    axios.get('https://api.sunrise-sunset.org/json?lat='+latitude+'&lng='+longitude+'&'+date+'&formatted=0')
                        .then(response => {
                            tunnid.push(Math.round(response.data['results']["day_length"]/3600*100)/100)
                        })
                        .catch(e => {
                            alert(e);
                        })
                });
                return tunnid;
            }
        }
    }
</script>

<style scoped>

</style>