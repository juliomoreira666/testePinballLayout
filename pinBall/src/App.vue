
<template>
<div>
<div class="header">
<div class="container">
<div class="logo"><img src="https://i.imgur.com/9LsG4wf.png"/></div>
<div class="seacrh"><input type="search" class="filtro" v-on:input="filtro = $event.target.value" placeholder="FILTRE PELO TITULO!"></div>
<div class="user"></div>
</div>
</div>
<div id="columns" class="container">
  <figure v-for="foto in fotosComFiltro">
  <img :src="foto.url" :alt="foto.titulo">
  <h1>{{ foto.titulo }}</h1>
  <figcaption>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce lacus sapien, ullamcorper</figcaption>
	</figure>
</div>
</div>
</template>

<script>

import Painel from './components/shared/painel/Painel.vue'

export default {

  components: {

    'meu-painel': Painel
  },

  data () {
    return {
      titulo: 'PinBall', 

      fotos: [],

      filtro: ''
    }
  },

  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
        // filtra a lista, por enquanto vamos retornar uma lista em branco
        return [];
      } else {
        // se o campo estiver vazio, não filtramos, retornamos a lista
        return this.fotos;
      }
    }
  },

  created() {

    this.$http
      .get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
}
</script>

<style>
@font-face{font-family:'Calluna';
 src:url('https://s3-us-west-2.amazonaws.com/s.cdpn.io/4273/callunasansregular-webfont.woff') format('woff');
}
body {
	background: url(//subtlepatterns.com/patterns/scribble_light.png);
  font-family: Calluna, Arial, sans-serif;
  min-height: 1000px;
}
#columns {
	column-width: 320px;
	column-gap: 15px;
  width: 90%;
	max-width: 1100px;
	margin: 50px auto;
}

div#columns figure {
	background: #fefefe;
	border: 2px solid #fcfcfc;
	box-shadow: 0 1px 2px rgba(34, 25, 25, 0.4);
	margin: 0 2px 15px;
	padding: 15px;
	padding-bottom: 10px;
	transition: opacity .4s ease-in-out;
  display: inline-block;
  column-break-inside: avoid;
}

div#columns figure img {
	width: 100%; height: auto;
	border-bottom: 1px solid #ccc;
	padding-bottom: 15px;
	margin-bottom: 5px;
}

div#columns figure figcaption {
  font-size: .9rem;
	color: #444;
  line-height: 1.5;
}

div#columns small { 
  font-size: 1rem;
  float: right; 
  text-transform: uppercase;
  color: #aaa;
} 

div#columns small a { 
  color: #666; 
  text-decoration: none; 
  transition: .4s color;
}

div#columns:hover figure:not(:hover) {
	opacity: 0.4;
}

@media screen and (max-width: 750px) { 
  #columns { column-gap: 0px; }
  #columns figure { width: 100%; }
}

html, body {
  height: 100%;
  width: 100%;
}
.header {
  padding: 20px;
  height: 50px;
  background-color: #ffffff;
  width: 100%;
  margin: 0 auto;
  position: relative;
}
.logo {
  float: left;
  width: 33.33%;
  position: relative;
}
.search {
  float: left;
  width: 33.33%;
  position: relative;

}
.user {
  float: left;
  width: 33.33%;
  position: relative;
}
.filtro {
  margin-top: 1px;
   box-sizing: border-box;
    border: 2px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
    background-color: white;
    background-position: 10px 10px; 
    background-repeat: no-repeat;
    padding: 12px 20px 12px 40px;
    -webkit-transition: width 0.4s ease-in-out;
    transition: width 0.4s ease-in-out;
 width: 30%;
}

.filtro:focus {
    width: 35%;
}
</style>
