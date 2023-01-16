<template>
  <div class='nax-card'>
    <div class='img-card'>
      <img v-if='isLoading' :src="img" loading='lazy' :width='widthSize' :height='imgHeight' @error='isLoading = false'>
    </div>

    <template v-if='!notext'>
      <div v-if="type === 'card'" class='text-card'>
        <div v-if='!text' class='sk-line'></div>
        <p v-else>{{ getText(text,23) }}</p> </div>

      <div v-else-if="type === 'search'" class='text-card'>
        <div v-if='!text' class='sk-line'></div>
        <p v-else>{{ getText(text,23) }}</p>
      </div>

      <div class="text-banner" v-else-if="type === 'Banner'">
        <div v-if='!title' class='sk-line'></div>
        <h2 v-else>{{getText(title,73)}}</h2>
        <div v-if='!text' class='sk-line Banner-text'></div>
        <p v-else>{{text}}</p>
      </div>
    </template>
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
    title: String,
    type: {
      type: String,
      default: 'card'
    },
    styles: Object
  })

  const isLoading = ref(true)

  let widthSize = 328
  let heightSize = 298
  let imgHeight = 238.5

  if (props.styles) {
    const {width,height} = props.styles
    widthSize = width
    heightSize = height
    imgHeight = height - 59.5
  }

  const getText = (text) => {
    let n = 23
    n = widthSize / 14
    return text.length > n ? text.substr(0,n) +'..' : text 
  }

  if (props.type === 'card-lg') {
    widthSize = 445
    heightSize = 737
    imgHeight = 570
  }

  else if (props.type === 'search') {
    widthSize = 288
    heightSize = 255
    imgHeight = 192
  }

  else if (props.type === 'Banner') {
    widthSize = 1280
    heightSize = 453
    imgHeight = 350
  }

  const widthCard = widthSize +'px'
  const heightCard = heightSize +'px'
  const imgContainer = imgHeight +'px'
</script>

<style>
.nax-card {
  width: v-bind(widthCard);
  height: v-bind(heightCard);
  border-radius: 6px;
  margin-right: 20px;
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
  .nax-card .text-card p {
    font-size: 24px;
    height: 28px;
    overflow: hidden;
    letter-spacing: 0.5px; }
  .nax-card .sk-line {
    display: flex;
    width: v-bind(widthCard);
    padding: 14px;
    background: #eee;
    border-radius: 5px; }
  .nax-card .text-card {
    border-radius: 6px;
    width: v-bind(width);
    height: 59.5px;
    display: flex;
    align-items: center; }
  .nax-card .text-banner {
    width: 80em;
    height: 74px;
    overflow: hidden;
    padding: 10px 0;
    align-items: center; }
  .nax-card .text-banner .sk-line {
    width: 22em}
  .nax-card .Banner-text.sk-line {
    width: 0;
    width: 22em;
    margin-top: 15px;
    padding: 14px 15em }
    .nax-card .text-banner h2{
      font-size: 30px; }
    .nax-card .text-banner p {
      margin-top: 5px;
      font-size: 19px; }

  .nax-card h2, p, .sk-line {
    margin: 0 20px; }
</style>