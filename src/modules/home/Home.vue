<template>
    <div class="my-4">
        <div class="container">
            <form>
                <div class="input-group">
                    <input type="text" class="form-control" placeholder="Search for movies"/>
                    <div class="input-group-append">
                        <button type="submit" class="btn btn-primary">Search</button>
                    </div>
                </div>
            </form>

            <div class="d-flex justify-content-center mt-4">
                <a v-for="(n,index) in 26" :key="'link'+index" href="#" class="px-2">{{String.fromCharCode(index+65)}}</a>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    name:'Home'
}
</script>