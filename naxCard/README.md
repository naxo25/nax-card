# nax-card

Componente de carta hecho para Vue 3 que considera la experiencia de usuario al actuar como carta y skeleton. Se puede configurar el tamaño o usar los tipos definidos y sino se agrega texto el modo es Skeleton por defecto.

### Ejemplo de uso

	<script setup>
	  import naxCard from 'naxCard'
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

	  const styles = {
	    'mid-card': {
	      width: 404,
	      height: 354
	    }
	  }
	</script>

	<template>
	  <div style="margin: auto; margin: 30px 0 30px 0;">
	    <div v-if='!isLoading' class='container'>
	      <naxCard
	        v-for='i in users' 
	        :img='i.picture.large'
	        :text='i.email'
	        :styles="styles['mid-card']"
	      /> 
	    </div>
	    <div v-else class='container'>
	      <naxCard
	        v-for='i in 4'
	        :styles="styles['mid-card']"/>
	    </div>

	    <div v-if='!isLoading' class='container'>
	      <naxCard
	        v-for='i in users' 
	        :img='i.picture.large'
	        :text='i.email'
	      /> 
	    </div>
	    <div v-else class='container'>
	      <naxCard
	        v-for='i in 4'
	      />
	    </div>

	    <div v-if='!isLoading' class='container'>
	      <naxCard
	        type='Banner'
	        title='Title Banner'
	        text='Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'
	        img='https://duckduckgo.com/assets/logo_header.v108.svg'
	      />
	      <naxCard
	        type='Banner'
	        :notext='true'
	        img='https://duckduckgo.com/assets/logo_header.v108.svg'/> 
	    </div>
	    <div v-else class='container'>
	      <naxCard type='Banner' v-for='i in 2'/>
	    </div>
	  </div>
	</template>

	<style>
	  .container {
	    margin: auto;
	    display: flex;
	    width: 95%;
	    flex-wrap: wrap;
	  }
	</style>


### Props

	img: String, default: ''

	styles: Object, ej: {width:394, height:254}

	type: String, default: 'card'

	noimg: Boolean

	notext: Boolean

	text: String
