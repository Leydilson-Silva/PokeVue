<template>
    <div id="pokemon">
        <div class="card">
            <span class="tag is-rounded is-light">{{ number }}</span>
            <div class="card-image">
                <figure class="">
                    <img :src="currentImg" alt="pokemon image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <span class="tag is-light">{{ pokemon.type }}</span>

                        <p class="title is-4">{{ name }}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar sprite</button>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.id = res.data.id;
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            // console.log(this.pokemon);
            // console.log(res.data.id);
        })
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: '',
                id: '',
            },
        }
    },
    props: {
        number: Number,
        name: String,
        url: String,
        id: Number,
    },
    filters: {
        
    },
    
    methods: {
        mudarSprite: function () {
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    },
}
</script>

<style>
#pokemon {
    margin-top: 2%;
}
</style>