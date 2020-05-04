<template lang="html">
  <div id="favourite_countries">
    <h2>Bucket List</h2>
    <ul>
      <li v-for="country in bucketList">{{country.name}} <img class="small-flag" :src="country.flag"/> <button v-if="!country.visited" v-on:click="updateList(country)">Visit!</button></li>
    </ul>
  </div>
</template>

<script>
import BucketService from '@/services/BucketService.js'
import {eventBus} from '@/main.js'
export default {
  name: 'bucket-list',
  props: ['bucketList'],
  methods: {
    updateList(country){
      const updatedCountry = {
        name: country.name,
        flag: country.flag,
        visited: true
      }
      eventBus.$emit('country-visited', updatedCountry)
      BucketService.updateBucketList(country._id, updatedCountry)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
