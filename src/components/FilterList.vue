<template>
    <div>
        <div class="cdFilterContainer">

            <div class="row mb-3">

                <div class="col-3">

                    <!-- Filtro per genere -->
                    <p class="text-white">Filtra per genere:</p>

                    <!-- Input select -->
                    <div class="input-group">
                        <select class="form-select" @click="getMusicGenres" v-model="genreSelected">
                            <option>All</option>
                            <option v-for="genre in genresList" :key="genre">{{genre}}</option>
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
                        <select class="form-select" @click="getArtistsList" v-model="artistSelected">
                            <option>All</option>
                            <option v-for="artist in artistsList" :key="artist">{{artist}}</option>
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
export default {
    name: "FilterList",

    data(){
        return {
            genresList: [],
            genreSelected: "All",
            artistsList: [],
            artistSelected: "All"
        }
    },

    props: {
        disksArray: Array,
    },

    methods: {
        getMusicGenres(){
            this.genresList = [];
            this.disksArray.forEach((disk) => {
                if(!this.genresList.includes(disk.genre)) {
                    this.genresList.push(disk.genre);
                }
            }
            )
        },
        getArtistsList(){
            this.artistsList = [];
            this.disksArray.forEach((disk) => {
                if(!this.artistsList.includes(disk.author)) {
                    this.artistsList.push(disk.author);
                }
            }
            )
        },
        onChangeGenre(){
            this.$emit("changeGenre", this.genreSelected);
        },
        onChangeArtist(){
            this.$emit("changeArtist", this.artistSelected);
        }
    }

}
</script>

<!-- --------------------------------------------------------------------------- -->

<style lang="scss" scoped>

@import "../assets/scss/variables";
@import "../assets/scss/filter"

</style>