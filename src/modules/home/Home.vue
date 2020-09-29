<template>
    <div class="my-4">
        <div class="container">
            <form>
                <div class="input-group">
                    <input type="text" class="form-control" placeholder="Search for movies">
                    <div class="input-group-append">
                        <button type="submit" class="btn btn-primary">Search</button>
                    </div>
                </div>
                <a href="#" class="d-block">Advanced Search</a>
                <div class="d-inline-flex mt-2">
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
            <div class="row"></div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Home',
}
</script>