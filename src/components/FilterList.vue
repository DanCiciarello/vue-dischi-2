<template>
    <div>
        <div class="cdFilterContainer">

            <div class="row mb-3">

                <div class="col-3">

                    <!-- Filtro per genere -->
                    <p class="text-white">Filtra per genere:</p>

                    <!-- Input select -->
                    <div class="input-group">
                        <select class="form-select" v-model="genreSelected">
                            <option>All</option>
                            <option v-for="genre in state.genresList" :key="genre">{{genre}}</option>
                        </select>
                        <div class="input-group-append">
                            <button class="btn btn-outline-light" type="button" @click="onChangeGenre">Filtra</button>
                        </div>
                    </div>

                </div>

                <div class="col-3 offset-6">
                    
                    <!-- Filtro per artista -->
                    <p class="text-white">Filtra per artista:</p>

                    <!-- Input select -->
                    <div class="input-group">
                        <select class="form-select" v-model="artistSelected">
                            <option>All</option>
                            <option v-for="artist in state.artistsList" :key="artist">{{artist}}</option>
                        </select>
                        <div class="input-group-append">
                            <button class="btn btn-outline-light" type="button" @click="onChangeArtist">Filtra</button>
                        </div>
                    </div>

                </div>

            </div>

        </div>
    </div>
</template>

<!-- --------------------------------------------------------------------------- -->

<script>

import {state} from "../store";

export default {
    name: "FilterList",

    data(){
        return {
            genreSelected: "All",
            artistSelected: "All",
        }
    },

    computed: {
        state(){
            return state
        }
    },

    methods: {
        onChangeGenre(){
            state.genreSelected = this.genreSelected;
        },
        onChangeArtist(){
            state.artistSelected = this.artistSelected;
        }
    }

}
</script>

<!-- --------------------------------------------------------------------------- -->

<style lang="scss" scoped>

@import "../assets/scss/variables";
@import "../assets/scss/filter"

</style>