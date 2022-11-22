<template>
<!-- <div class="container">
    <div class="row">
        <div class="col-md-3">go</div>
        <div class="col-md-3">come</div>
        <div class="col-md-3">come</div>
        <div class="col-md-3">come</div>
    </div>
</div> -->
<div class="container">
    <div v-if="show_country_details" class="row">
        <div class="col-12">
            <h3 class="text-left" @click="show_country_details=false">All countries</h3>
        </div>
        <div class="col-md-4">
            <div class="card mb-4 mx-auto" style="width: 25rem;">
                <img :src="one_country.flags.png" class="card-img-top" alt="Country Flag">
                <div class="card-body">
                    <h5 class="card-title">{{one_country.name.common}}</h5>
                    <p class="card-text">Population: {{one_country.population}}</p>
                    <p class="card-text">Continent: {{one_country.continents[0]}}</p>
                </div>
            </div>
        </div>
    </div>
    <div v-else class="row">
        <div class="col-12">

            <h1 class="text-center">{{title}}.</h1>
        </div>
        <div class="col-sm-12 col-md-3 bg-success">
            <div v-if="countries.length > 0">
                <div class="card mb-4" v-for="(items, i) in countries" :key="i">
                    <img :src="items.flags.png" class="card-img-top" alt="Country Flag">
                    <div class="card-body">
                        <h5 class="card-title">{{items.name.common}}</h5>
                        <p class="card-text">Population: {{items.population}}</p>
                        <p class="card-text">Continent: {{items.continents[0]}}</p>
                        <a href="#" class="btn btn-primary" @click.prevent="showCountry(items.ccn3)">Show Country</a>
                    </div>
                </div>
            </div>
            <div v-else>
                <h1 class="text-center text-danger">Data has not loaded.</h1>
            </div>
        </div>
    </div>

</div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'App',
    data() {
        return {
            title: 'List of Countries',
            countries: [],
            one_country: [],
            show_country_details: false
        }
    },
    methods: {
        fetchData: function () {
            const api = 'https://restcountries.com/v3.1/all';
            axios.get(api)
                .then(res => {
                    this.countries = res.data;
                    console.log(this.countries);
                });
        },

        showCountry(id) {
            //   console.log(id);
            let a_country = this.countries.filter(country => country.ccn3 == id);
            this.one_country = a_country[0];
            console.log(this.one_country);
            this.show_country_details = true;
        }
    },
    created() {
        this.fetchData();
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}

[v-cloak] {
    display: none;
}
</style>
