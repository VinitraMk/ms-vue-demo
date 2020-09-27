<template>
    <div class="vd-card">
        <div class="vd-card__img">
            <img :src="imgSrc" :alt="title"/>
        </div>
        <div class="vd-card__title">
            {{title}}
        </div>
        <button class="btn btn-primary">View More</button>
    </div>
</template>
<script>
export default {
    name:"Card",
    props:{
        title:String,
        imgSrc:String
    }
}
</script>