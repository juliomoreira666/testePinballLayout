
<template>
<div>
  <div class="header">
    <div class="container-header">
      <div class="logo">
        <img src="https://i.imgur.com/9LsG4wf.png" />
      </div>
      <div class="menu">
        <img src="https://i.imgur.com/oUlCbi2.png" />
      </div>
      <div class="seacrh"><input type="input" class="filtro" v-on:input="filtro = $event.target.value" placeholder=""></div>
      <div class="user">
        <img src="https://i.imgur.com/VZ9inpG.png" />
        <span class="welcome">Welcome John</span>
      </div>
    </div>
  </div>
  <div id="columns" class="container">
    <figure v-for="foto in fotosComFiltro">
      <img :src="foto.url" :alt="foto.titulo">
      <h1>{{ foto.titulo }}</h1>
      <div class="locale"><img src="https://i.imgur.com/6y3tK5z.png" />Movies</div>
      <figcaption>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce lacus sapien, ullamcorper</figcaption>
      <div class="rating-face">
        <div class="rating">
        <i class="far fa-star voted"></i>
        <i class="far fa-star voted"></i>
        <i class="far fa-star no-voted"></i>
        <i class="far fa-star no-voted"></i>
        <img class="faceico" src="https://i.imgur.com/ZJk2Y7n.png"/>
      </div>
      </div>
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

$('.rating input').change(function () {
  var $radio = $(this);
  $('.rating .selected').removeClass('selected');
  $radio.closest('label').addClass('selected');
});

</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

.faceico {
  width: 21px!important;
  height: 21px!important;
  float: right;
}
i.voted {
  color: #b9cb41;
}
i.no-voted {
  color: #dddddd;
}

.rating-face {
      padding: 15px;
}
i 
{
  font: 18px/1 FontAwesome;
}
body {
  background-color: #f0efee;
  font-family: 'Open Sans', sans-serif;
  min-height: 1000px;
}
#columns {
	column-width: 260px;
	column-gap: 15px;
  width: 90%;
	max-width: 1100px;
	margin: 50px auto;
}

#columns h1, figcaption {
  padding: 15px;
}

.locale img {
  border: none!important;
  margin: 0 auto!important;
  padding: 0!important;
  margin-right: 10px!important;
  width: 9px!important;
  height: 12px!important;
}

.locale {
  padding: 14px;
    color: #acaaaa;
    font-size: 13.99px;
}



#columns h1 {
font-size: 17.99px;
 color: #717171;
}


div#columns figure {
	background: #fefefe;
	border: 2px solid #fcfcfc;
	box-shadow: 0 1px 2px rgba(34, 25, 25, 0.5);
	margin: 0 2px 15px;
	padding: 0px;
	padding-bottom: 0px;
	transition: opacity .4s ease-in-out;
  display: inline-block;
  column-break-inside: avoid;
  border-radius: 5px;
}

div#columns figure img {
	width: 100%; height: auto;
  /*border-bottom: 1px solid #ccc;*/
	padding-bottom: 15px;
	margin-bottom: 5px;
}

div#columns figure figcaption {
  font-size: 13px;
	color: #acaaaa;
  line-height: 1.5;
  text-align: justify;
  border-bottom: 1px solid #e9e9e9;
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
   border-bottom: 1px solid #d6d5d4;
   box-shadow: 1px  1px #d6d5d4;
   position: relative;
    height: 100px;
    background-color: #ffffff;
    width: 100%;
    margin: 0 auto;
    left: 0;
    top: 0;

}
.header div {
  padding: 0.99999999em;
}
.logo {
  cursor: pointer;
  float: left;
  width: 15%;
  position: relative;
}
.menu {
 float: left;
  width: 10%;
  text-align: center;
  position: relative;
  padding: 18px!important;
}

.menu img {
  cursor: pointer;
}
.seacrh {
     float: left;
    width: 33%;
    position: relative;

}
.user {
  float: right;
    width: 19%;
    position: relative;
}
.filtro {
  box-shadow: 0px  1px #d6d5d4;
  margin-top: 1px;
   box-sizing: border-box;
    border: 1px solid #e7e7e7;
    border-radius: 5px;
    font-size: 16px;
    background-color: #f7f6f6;
    background-position: 10px 10px; 
    background-repeat: no-repeat;
    padding: 12px 20px 12px 40px;
    -webkit-transition: width 0.4s ease-in-out;
    transition: width 0.4s ease-in-out;
    width: 430px;
    height: 34px;
    background-image: url('https://i.imgur.com/eYjXDi0.png');
    background-position: 97% 7px;
    cursor: pointer;


}
.container-header {
    width: 90%;
    max-width: 1100px;
    margin: 0 auto;
}

.filtro:focus {
    width: 80%;
}

.welcome {
  float: right;
  margin: 10px auto;
  width: 72%;
  color: #8c8c8c;
  cursor: pointer;
}



/* Normalize CSS */

/*! normalize.css v8.0.0 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

h1 {
  margin: 0px!important;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */


/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}
</style>
