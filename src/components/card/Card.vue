<template>
    <div class="vd-card">
        <div class="vd-card__img">
            <img v-if="imgSrc==='N/A'" src="../../assets/poster_placeholder.jpg" :alt="title"/>
            <img v-if="imgSrc!=='N/A'" :src="imgSrc" :alt="title"/>
        </div>
        <div class="vd-card__title">
            {{title}}
        </div>
        <button class="btn btn-primary" @click="showDetails">View More</button>
    </div>
</template>
<script>
export default {
    name:"Card",
    props:{
        title:String,
        imgSrc:String,
        id:String
    },
    methods: {
        showDetails() {
            this.$emit('showMore',this.id);
        }
    },
}
</script>