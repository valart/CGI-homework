<template>
    <l-map ref="myMap" :zoom="zoom" :center="coordinates" @click="updateCoordinates">
        <l-tile-layer :url="url"></l-tile-layer>
        <l-marker :lat-lng="coordinates" ></l-marker>
    </l-map>
</template>

<script>
    export default {
        props: {
            latitude: Number,
            longitude: Number
        },
        data () {
            return {
                url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
                zoom: 16,
                lat:this.latitude,
                lng:this.longitude
            };
        },
        methods: {
            updateCoordinates(event){
                this.lat=event.latlng['lat'];
                this.lng=event.latlng['lng'];
                this.$emit("coordinates",[this.lat,this.lng])
            }
        },
        computed: {
            coordinates: function () {

                if(this.lat===null || this.lng===null)
                    return [58.3648016, 26.7393249];
                else {
                    return [this.lat, this.lng];
                }
            }
        },
        watch: {
            latitude(){
                this.lat=this.latitude;
            },
            longitude(){
                this.lng=this.longitude
            }
        }
    }
</script>

<style scoped>

</style>