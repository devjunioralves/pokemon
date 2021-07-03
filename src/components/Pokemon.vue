<template>
  <div id="pokemon">
    <h1></h1>
    <small>{{ url }}</small>

    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="currentImg"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name | upperName }}</p>
            <p class="subtitle is-6"> {{ pokemon.type }}</p>
          </div>
        </div>
        <div class="content"></div>
            <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function() {
    axios.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      pokemon: {
          type: '',
          front: '',
          back: ''
      },
      isFront: true,
      currentImg: '',
    };
  },
  name: "Pokemon",
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upperName: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
      mudarSprite: function(){
          if(this.isFront){
              this.isFront = false;
              this.currentImg = this.pokemon.back
          }
          else{
              this.isFront = true;
              this.currentImg = this.pokemon.front
          }
      }
  }
};
</script>

<style>

#pokemon{
    margin-top: 2%;
}

</style>
