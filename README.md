# nax-card

Card hecha en Vue usable como skeleton para experiencia de usuario y carta básica para imagen, datos. Sino se agrega nada el modo es Skeleton por defecto.

Vue 3 + Vite: This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

![](./sample/img1.png)

![](./sample/img2.png)

### Ejemplo de uso

	<template>
	  <div style="margin: auto; margin-bottom: 60px;">
	    <div v-if='!isLoading' class='container'>
	      <naxCard v-for='i in users' :img='i.picture.large' :text='i.email'/> 
	    </div>
	    <div v-else class='container'>
	      <naxCard v-for='i in 4'/>
	    </div>

	    <div v-if='!isLoading' class='container'>
	      <naxCard
	        type='Banner' 
	        titleBanner='Title Banner' 
	        text='Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.' 
	        img='https://duckduckgo.com/assets/logo_header.v108.svg'
	      />
	      <naxCard type='Banner' :notext='true' img='https://duckduckgo.com/assets/logo_header.v108.svg'/> 
	    </div>
	    <div v-else class='container'>
	      <naxCard type='Banner' v-for='i in 2'/>
	    </div>
	  </div>
	</template>

	<script setup>
	  import naxCard from 'nax-card'
	  import {ref} from 'vue'

	  const users = ref({})
	  const isLoading = ref(true)

	  setTimeout(() => {
	    fetch('https://randomuser.me/api/?results=4').then(async response => {
	      const data = await response.json()
	      users.value = data.results
	      isLoading.value = false
	    })
	  }, 1000)
	</script>

	<style>
	  .container {
	  	margin: auto;
	  	display: flex;
	  	flex-wrap: wrap;
	  	width: 80%;
	  }
	</style>


### Props

	img: String, default: ''

	noimg: Boolean

	notext: Boolean

	text: String

	type: String, default: 'card'
