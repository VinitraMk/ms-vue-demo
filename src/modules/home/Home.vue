<template>
    <div class="my-4">
        <div class="container">
            <form>
                <div class="input-group">
                    <input type="text" class="form-control" placeholder="Search for movies" v-model="searchString"/>
                    <div class="input-group-append">
                        <button type="submit" class="btn btn-primary" @click="searchForTitle($event)">Search</button>
                    </div>
                </div>
                <a href="#" class="d-block" v-on:click="toggleFilters()">Advanced Search</a>
                <div class="d-inline-flex mt-2" v-if="showFilters">
                    <label class="mr-2">Filter By</label>
                    <select class="form-control">
                        <option>--Select--</option>
                        <option>Movies</option>
                        <option>Series</option>
                    </select>
                </div>
            </form>
        </div>

        <div class="vd-container">
            <div class="row">
                {{movieList}}
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

let apiKey = "37b8c8a7";
let omdbUrl = "http://www.omdbapi.com";
let defaultId = "tt3896198";
export default {
    name:'Home',
    components: {
    },
    data() {
        return {
            movieList:[],
            showFilters:false,
            searchString:"",
            showModal:false,
            selectedMovie:{
                Title:"",
                Plot:""
            }
        }
    },

    mounted() {
        let apiUrl = `${omdbUrl}?i=${defaultId}&apikey=${apiKey}`;
        this.getData(apiUrl);
    },

    methods: {
        getData(url) {
            axios.get(url).then(res=>{
                this.movieList = [res.data];
            });
        },
        toggleFilters() {
            this.showFilters = !this.showFilters;
        },
    },
}
</script>