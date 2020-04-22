<template>
    <div>
        <div class="viewport">
            <md-toolbar :md-elevation="1">
                <span class="md-title">Sisestage andmed</span>
            </md-toolbar>

            <md-list class="md-double-line">
                <md-subheader>Koordinaadid</md-subheader>

                <md-list-item>
                    <md-field>
                        <label>Geograafilise laiuse</label>
                        <md-input placeholder="Geograafilise laiuse" type="number" :value="latitude" @change="getLat"></md-input>
                    </md-field>
                </md-list-item>

                <md-list-item>
                    <md-field>
                        <label>Geograafilise pikkus</label>
                        <md-input placeholder="Geograafilise pikkus" type="number" :value="longitude" @change="getLng"></md-input>
                    </md-field>
                </md-list-item>

                <md-divider></md-divider>
                <md-subheader>Kuupäevad</md-subheader>

                <md-list-item>
                    <md-datepicker v-model="date" format="yyyy-MM-dd" md-immediately>
                        <label>Valige kuupäev</label>
                    </md-datepicker>
                </md-list-item>

                <md-list-item>
                    <md-datepicker v-model="date2" format="yyyy-MM-dd" md-immediately>
                        <label>Valige teine kuupäev</label>
                    </md-datepicker>
                </md-list-item>
            </md-list>
            <md-button class="md-raised md-primary" v-on:click="checkInput">Otsi</md-button>
        </div>
        <md-dialog :md-active.sync="showDialog" style="width: 490px">
            <md-dialog-content>
                <table>
                    <tr>
                        <td><md-icon class="md-size-2x">arrow_upward</md-icon> Päikese tõus</td>
                        <td style="text-align: right;">{{sunrise}}</td>
                    </tr>
                    <tr>
                        <td><md-icon class="md-size-2x">arrow_downward</md-icon> Päikese loojang</td>
                        <td style="text-align: right;">{{sunset}}</td>
                    </tr>
                    <tr>
                        <td><md-icon class="md-size-2x">wb_sunny</md-icon> Päev kestab</td>
                        <td style="text-align: right;">{{day_length}}</td>
                    </tr>
                </table>
            </md-dialog-content>
        </md-dialog>

        <md-dialog :md-active.sync="showChart">
            <md-dialog-content>
                <graphics :latitude="latitude" :longitude="longitude" :date="date" :date2="date2"/>
            </md-dialog-content>
        </md-dialog>

    </div>
</template>

<script>
    import moment from 'moment';
    import graphics from "./graphics";
    import axios from 'axios';

    export default {
        name: "inputs",
        components: {graphics},
        props: {
            latitude: Number,
            longitude: Number
        },
        data () {
            return {
                lat: this.latitude,
                lng: this.longitude,
                date: null,
                date2: null,
                showDialog: false,
                showChart: false,
                sunrise: null,
                sunset:null,
                day_length:null,
            };
        },
        methods:{
            getLat(event) {
                this.$emit("latitude",event.target.value)
            },
            getLng(event) {
                this.$emit("longitude",event.target.value)
            },
            checkInput: function(){
                if(this.latitude !== null && this.longitude !== null && this.date !== null && this.date2!==null){
                    this.showChart=true;
                }
                else if(this.latitude !== null && this.longitude !== null && this.date !== null){
                    this.showDialog=true;
                    let date = moment(String(this.date)).format("YYYY-MM-DD");
                    axios.get('https://api.sunrise-sunset.org/json?lat='+this.latitude+'&lng='+this.longitude+'&'+date)
                        .then(response => {
                            this.sunrise=response.data['results']["sunrise"];
                            this.sunset=response.data['results']["sunset"];
                            this.day_length=response.data['results']["day_length"];
                        })
                        .catch(e => {
                            alert(e)
                        })
                }
                return;
            }
        }
    }
</script>

<style scoped>
    .viewport {
        width: 320px;
        max-width: 100%;
        display: inline-block;
        vertical-align: top;
        overflow: auto;
        border: 1px solid lightgray;
        max-height: 95%;
    }
    td{
        font-size: 20px;
        width: 200px;
    }
</style>