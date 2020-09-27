<template>
    <div class="my-4">
        <div class="container">
            <form v-on:submit="searchForTitle()">
                <div class="input-group">
                    <input type="text" class="form-control" placeholder="Search for movies" :value="titleInput" @input="titleInputHandler($event)"/>
                    <div class="input-group-append">
                        <button type="submit" class="btn btn-primary">Search</button>
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
            <p>{{resultSummary}}</p>
        </div>

        <div class="vd-container">
            <Card v-for="(movie,index) in movieList" :key="`${movie.Title}-${index}`" :title="movie.Title" :imgSrc="movie.Poster"/>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import Card from "../../components/card/Card";

var apiUrl = "http://www.omdbapi.com/?i=tt3896198&apikey=37b8c8a7";
export default {
    name:'Home',
    components: {
        Card
    },
    data() {
        return {
            movieList:[],
            showFilters:false,
            titleInput:""
        }
    },

    mounted() {
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
        titleInputHandler(e) {
            this.titleInput = e.target.value;
        },
        searchForTitle() {
            if(this.titleInput!=="") {
                let searchParam = this.titleInput;
                if(this.titleInput.indexOf(" ")>-1) {
                    searchParam = searchParam.split(" ").join("+")
                }
                let tempUrl = apiUrl + "&s="+searchParam;
                axios.get(tempUrl).then((res)=>{
                    console.log(res.data.search);
                    this.movieList = [...res.data.Search];
                });
            }
            else {
                this.getData(apiUrl);
            }
        }
    },
    computed: {
        resultSummary() {
            if(this.movieList.length===1) {
                return "Showing 1 result";
            }
            else {
                return `Showing ${this.movieList.length} results`;
            }
        }
    }


}
</script>