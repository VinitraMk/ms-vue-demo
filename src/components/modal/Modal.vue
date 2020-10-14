<template>
    <div v-if="showModal" class="vd-modal" tabindex="-1">
        <div class="vd-modal-dialog">
            <div class="vd-modal__header">
                <h5 class="vd-modal__title">{{title}}</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="closeModal">
                    <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="vd-modal__body">
            </div>
            <div class="vd-modal__footer">
                <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="closeModal">Close</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Modal'
}
</script>