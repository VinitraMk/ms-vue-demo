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
                <a href="#" class="d-block" @click="toggleFilters">Advanced Search</a>
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
                <div class="col-md-2" v-for="(movie,index) in movieList" :key="`movie-${index}`">
                    <Card :title="movie.Title" :imgSrc="movie.Poster" :id="movie.imdbID" @viewMore="showPlot"></Card>
                </div>
            </div>
        </div>
        <Modal :title="selectedMovie.Title" :showModal="displayModal" @onDismiss="closeModal">
            <p>{{selectedMovie.Plot}}</p>
        </Modal>
    </div>
</template>

<script>
import axios from "axios";
import Card from "../../components/card/Card";
import Modal from "../../components/modal/Modal";

let apiKey = "37b8c8a7";
let omdbUrl = "http://www.omdbapi.com";
let defaultId = "tt3896198";
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
            selectedMovie:{
                Title:""
            },
            displayModal:false
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
        searchForTitle(e) {
            e.preventDefault();
            if(this.searchString!=="") {
                let apiUrl = `${omdbUrl}?i=${defaultId}&apikey=${apiKey}&s=${this.searchString}`;
                axios.get(apiUrl).then(res=>{
                    this.movieList = [...res.data.Search];
                });
            }
        },
        showPlot(id) {
            let apiUrl = `${omdbUrl}?i=${id}&apikey=${apiKey}`;
            axios.get(apiUrl).then(res=>{
                this.selectedMovie = res.data;
                this.displayModal = true;
            });
        },
        closeModal() {
            this.displayModal = false;
        }
    },
}
</script>