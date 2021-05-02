<template>
  <div id="pokemon" class="card">
    <div class="card-image">
      <figure>
        <img @mouseover="mudarSprite" @mouseout="mudarSprite" :src="currentImg" width="30%" :alt="name" />
      </figure>
    </div>

    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ num }}-{{ name }}</p>
          <p class="subtitle is-6">{{ pokemon.type }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.currentImg = this.pokemon.front
      })
      .catch((err) => console.log(err));
  },
  name: "pokemon",
  data() {
    return {
      currentImg: "",
      isFront: true,
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function (value) {
      let newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
    mudarSprite: function () {
      console.log("clicou");
      if(this.isFront){
          this.currentImg = this.pokemon.back
          this.isFront = false
      }else{
          this.currentImg = this.pokemon.front
          this.isFront = true
      }      
    },
  },
};
</script>

<style>
#pokemon {
  margin-top: 2%;
}
</style>