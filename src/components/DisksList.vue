<template>
    <div class="cdDisksListsContainer py-5">
        <div class="container">

            <!-- Sezione filtri -->
            <FilterList/>

            <!-- Lista dischi -->
            <div class="row row-cols-5 gx-5 gy-4 mt-3">

                <!-- Ciclo i dischi -->
                <div class="col" v-for="disk in getDisksFiltered" :key="disk.title">
                    <DiskItem :disk-obj="disk" />
                </div>

            </div>

            <div v-if="getDisksFiltered.length === 0">
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
import {state} from "../store";

export default {
    name: "DisksList",
    data() {
        return {
            apiUrl: "https://flynn.boolean.careers/exercises/api/array/music",
            disksArray: [],
        };
    },
    computed: {
        getDisksFiltered(){
            // Se è selezionato All
            if(state.genreSelected === "All" && state.artistSelected === "All"){
                // Ritorno l'array completo
                return this.disksArray;
            } 
            // Se selezionato un genere
            else if(state.genreSelected !== "All" && state.artistSelected === "All") {
                // Filtro l'array originale per genere
                return this.disksArray.filter(disk => {
                    return disk.genre.includes(state.genreSelected);
                })
            } 
            // Se selezionato un artista
            else if(state.genreSelected === "All" && state.artistSelected !== "All") {
                // Filtro l'array originale per artista
                return this.disksArray.filter(disk => {
                    return disk.author.includes(state.artistSelected);
                })
            } 
            // Se selezionati entrambi
            else {
                // Filtro l'array originale per genere e artista
                return this.disksArray.filter(disk => {
                    return disk.genre.includes(state.genreSelected) && disk.author.includes(state.artistSelected);
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
                    this.getMusicGenres();
                    this.getArtistsList();
            });
        },
        getMusicGenres(){
            state.genresList = [];
            this.disksArray.forEach((disk) => {
                if(!state.genresList.includes(disk.genre)) {
                    state.genresList.push(disk.genre);
                }
            }
            )
        },
        getArtistsList(){
            state.artistsList = [];
            this.disksArray.forEach((disk) => {
                if(!state.artistsList.includes(disk.author)) {
                    state.artistsList.push(disk.author);
                }
            }
            )
        },
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