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
                <a href="#" class="d-block mb-2" v-on:click="toggleFilters()">Advanced Search</a>
                <div class="vd-form-group vd-collapsible" :class="{active:showFilters}">
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
            <div class="row">
                <div class="col-md-2" v-for="(movie,index) in movieList" :key="`${movie.Title}-${index}`">
                    <Card  :title="movie.Title" :imgSrc="movie.Poster" :id="movie.imdbID" v-on:showMore="showPlot"/>
                </div>
            </div>
        </div>
        <Modal :showModal="showModal" v-on:onDismiss="closeModal" :title="selectedMovie.Title">
            {{selectedMovie.Plot}}
        </Modal>
    </div>
</template>

<script>
import axios from "axios";
import Card from "../../components/card/Card";
import Modal from "../../components/modal/Modal";

var apiUrl = "http://www.omdbapi.com/?i=tt3896198&apikey=37b8c8a7";
let apiKey = "37b8c8a7";
let ombdUrl = "http://www.omdbapi.com";
export default {
    name:'Home',
    components: {
        Card,
        Modal
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
        searchForTitle(e) {
            e.preventDefault();
            if(this.searchString!=="") {
                let searchParam = this.searchString;
                if(this.searchString.indexOf(" ")>-1) {
                    searchParam = searchParam.split(" ").join("+")
                }
                let tempUrl = apiUrl + "&s="+searchParam;
                axios.get(tempUrl).then((res)=>{
                    console.log(res.data);
                    this.movieList = [...res.data.Search];
                });
            }
            else {
                this.getData(apiUrl);
            }
        },
        closeModal() {
            this.showModal = !this.showModal;
        },
        showPlot(id) {
            console.log(id);
            let tempUrl = `${ombdUrl}?i=${id}&apikey=${apiKey}`;
            console.log(tempUrl);
            axios.get(tempUrl).then((res)=>{
                this.selectedMovie = res.data;
                this.showModal = true;
            });
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