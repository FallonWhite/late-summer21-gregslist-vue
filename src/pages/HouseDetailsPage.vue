<template>
  <div class="house bg-light shadow">
    <h1>Welcome to the house details</h1>
    <img :src="house.imgUrl">
    <div class="p-3">
      <div class="text-center">
        {{ house.price }}<br />
        {{ house.bedrooms }} Bedrooms, - {{ house.bathrooms }} Bathrooms<br />
        Built {{ house.year }}, Levels {{ house.levels }}<br />
      </div>
      <p>{{house.description}}</p>
      <p><em>{{house.price}}</em></p>
    </div>
    <button class="btn btn-danger" @click="destroy">Delete</button>
  </div>
</template>

<script>
import { computed, onMounted } from '@vue/runtime-core'
import { AppState } from '../AppState'
import { housesService } from '../services/HousesService'
import {useRoute, useRouter} from 'vue-router'
export default {
  setup(){
    const route = useRoute()
    const router = useRouter()
    onMounted(async()=>{
      try {
        await housesService.getHouseById(route.params.id)
      } catch (error) {
        console.error(error)
      }
    })
    return {
      house: computed(()=> AppState.activeHouse),
      async destroy(){
        try {
          await housesService.destroy(route.params.id)
          //  navigate user back to home
          router.push({name: 'House'})
        } catch (error) {
          console.error(error)
        }
      }
    }
  }}
</script>


<style>
</style>