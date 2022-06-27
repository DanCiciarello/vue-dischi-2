<template>
    <div class="cdDiskItemContainer text-center">
        <img :src="diskObj.poster" :alt="diskObj.title" class="cdDiskPoster mb-3">
        <h6 class="text-uppercase text-white"><strong>{{diskObj.title}}</strong></h6>
        <span class="cdDiskSubtitle">{{diskObj.author}}</span>
        <span class="cdDiskSubtitle">{{diskObj.year}}</span>
    </div>
</template>

<!-- --------------------------------------------------------------------------- -->

<script>
export default {
    name: "DiskItem",
    props: {
        diskObj: Object,
    }
}
</script>

<!-- --------------------------------------------------------------------------- -->

<style lang="scss">

@import "../assets/scss/variables";
@import "../assets/scss/disk";

</style>