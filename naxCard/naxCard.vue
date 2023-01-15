<template>
  <div class='nax-card'>
    <div class='img-card'>
      <img v-if='isLoading' :src="img" loading='lazy' :width='width' :height='imgHeight' @error='isLoading = false'>
    </div>

    <div v-if="type === 'card'" class='text-card'>
      <div v-if='!text && !notext' class='line'></div>
      <p v-else>{{text.length > 23 ? text.substr(0,23)+'...' : text }}</p>
    </div>

    <div v-else-if="type === 'search'" class='text-card'>
      <div v-if='!text && !notext' class='line'></div>
      <p v-else>{{text.length > 23 ? text.substr(0,23)+'...' : text }}</p>
    </div>

    <div class="text-banner" v-else-if="type === 'Banner'">
      <div v-if='!titleBanner && !notext' class='line'></div>
      <h2 v-else>{{titleBanner}}</h2>
      <div v-if='!text && !notext' class='line Banner-text'></div>
      <p v-else>{{text}}</p>
    </div>
  </div>
</template>

<script setup>
  import {ref} from 'vue'

  const props = defineProps({
    img: {
      type: String,
      default: ''
    },
    noimg: Boolean,
    notext: Boolean,
    text: String,
    titleBanner: String,
    type: {
      type: String,
      default: 'card'
    }
  })

  const isLoading = ref(true)

  let width = 328
  let height = 298
  let imgHeight = 238.5

  if (props.type === 'card-lg') {
    width = 445
    height = 737
    imgHeight = 570
  }

  else if (props.type === 'search') {
    width = 288
    height = 255
    imgHeight = 192
  }

  else if (props.type === 'Banner') {
    width = 1280
    height = 453
    imgHeight = 350
  }

  const widthCard = width +'px'
  const heightCard = height +'px'
  const imgContainer = imgHeight +'px'
</script>

<style>
.nax-card {
  width: v-bind(widthCard);
  height: v-bind(heightCard);
  border-radius: 6px;
  margin: 27px 20px 0 0px;
  color: #000;
  background-color: #fff; }
  .nax-card .img-card {
    width: v-bind(widthCard);
    max-width: v-bind(widthCard);
    height: v-bind(imgContainer);
    border-radius: 6px;
    background-color: #eee; }
    .nax-card .img-card img {
      border-radius: 6px;
      background-color: #eee;
      object-fit: unset; }
  .nax-card p {
    margin: 0px;
    margin-left: 20px;
    font-family: SamsungOne;
    font-size: 24px;
    font-weight: bold;
    letter-spacing: 0.5px;
    overflow: hidden;
    text-overflow: ellipsis; }
  .nax-card .line {
    display: flex;
    width: 80px;
    margin-left: 20px;
    padding: 14px 9em;
    background: #eee;
    border-radius: 5px; }
  .nax-card .Banner-text {
    width: 200px;
    margin-top: 15px;
    padding: 14px 15em }
  .nax-card .text-card {
    border-radius: 6px;
    width: v-bind(width);
    height: 59.5px;
    display: flex;
    align-items: center; }
  .nax-card .text-banner {
    width: 80em;
    height: 76px;
    padding: 10px 0;
    align-items: center; }
    .nax-card .text-banner h2{
      font-size: 30px;
      margin: 0px;
      margin-left: 22px; }
    .nax-card .text-banner p {
      margin-top: 5px;
      margin-left: 22px;
      font-size: 19px; }
</style>