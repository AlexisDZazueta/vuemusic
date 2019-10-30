<template>
  <li>
    <h2><a :href="artist.url" target="_blank">{{ artist.name }}</a></h2>
    <img :src="artist.image[2]['#text']" :alt="artist.name">
  </li>
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]
}
</script>

<style>
  li {
    display: block;
    margin: 10px 0;
  }
</style>
