<template>
    <div class="cdDisksListsContainer py-5">
        <div class="container">

            <!-- Sezione filtri -->
            <FilterList :disks-array="disksArray" @changeGenre="onChangeGenre" @changeArtist="onChangeArtist" />

            <!-- Lista dischi -->
            <div class="row row-cols-5 gx-5 gy-4 mt-3">

                <!-- Ciclo i dischi -->
                <div class="col" v-for="disk in getDisksFiltered" :key="disk.title">
                    <DiskItem :disk-obj="disk" />
                </div>

            </div>

            <div v-if="getDisksFiltered.length == 0">
                <div class="alert alert-danger" role="alert">
                    Mi spiace, non ci sono risultati con i filtri selezionati!
                </div>
            </div>

        </div>
    </div>
</template>

<!-- --------------------------------------------------------------------------- -->

<script>

import axios from "axios";
import DiskItem from "./DiskItem.vue";
import FilterList from "./FilterList.vue";

export default {
    name: "DisksList",
    data() {
        return {
            apiUrl: "https://flynn.boolean.careers/exercises/api/array/music",
            disksArray: null,
            genresList: [],
            genreSelected: "All",
            artistSelected: "All"
        };
    },
    computed: {
        getDisksFiltered(){
            // Se è selezionato All
            if(this.genreSelected === "All" && this.artistSelected === "All"){
                // Ritorno l'array completo
                return this.disksArray;
            } 
            // Se selezionato un genere
            else if(this.genreSelected !== "All" && this.artistSelected === "All") {
                // Filtro l'array originale per genere
                return this.disksArray.filter(disk => {
                    return disk.genre.includes(this.genreSelected);
                })
            } 
            // Se selezionato un artista
            else if(this.genreSelected === "All" && this.artistSelected !== "All") {
                // Filtro l'array originale per artista
                return this.disksArray.filter(disk => {
                    return disk.author.includes(this.artistSelected);
                })
            } 
            // Se selezionati entrambi
            else {
                // Filtro l'array originale per genere e artista
                return this.disksArray.filter(disk => {
                    return disk.genre.includes(this.genreSelected) && disk.author.includes(this.artistSelected);
                })

            }
        }
    },
    methods: {
        fetchDisksList() {
            // Chiamo l'API e valorizzo l'array con i risultati
            axios
                .get(this.apiUrl)
                .then((result) => {
                    this.disksArray = result.data.response;
            });
        },
        onChangeGenre(genreSelected){
            this.genreSelected = genreSelected;
        },
        onChangeArtist(artistSelected){
            this.artistSelected = artistSelected;
        }
    },
    mounted() {
        this.fetchDisksList();
    },
    components: { DiskItem, FilterList }
}
</script>

<!-- --------------------------------------------------------------------------- -->

<style lang="scss">

</style>