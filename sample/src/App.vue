<script setup>
  import naxCard from '../../naxCard'
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
      <naxCard type='Banner'/>
      <naxCard type='Banner'/>
    </div>
  </div>
</template>

<style>
  .container {
    margin: auto; display: flex; width: 80%; flex-wrap: wrap;
  }
</style>