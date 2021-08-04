<template>
  <div class="house-form">
    <form class="d-flex" @submit.prevent="createHouse">
      <div class="form-group">
        <label for="bedrooms">Bedrooms</label>
        <input 
          type="number" 
          name="bedrooms" 
          v-model="state.newHouse.bedrooms"
          class="form-control"
          placeholder="Bedrooms..." 
          required>
      </div>
      <div class="form-group">
        <label for="bathrooms">Bathrooms</label>
        <input 
          type="number" 
          name="bathrooms" 
          v-model="state.newHouse.bathrooms"
          class="form-control" 
          placeholder="Bathrooms..."
          required>
      </div>
      <div class="form-group">
        <label for="levels">Levels</label>
        <input 
          type="number" 
          name="levels" 
          v-model="state.newHouse.levels"
          class="form-control" 
          placeholder="Levels..."
          required>
      </div>
      <div class="form-group">
        <label for="year">Year Built</label>
        <input 
          type="number" 
          name="year" id="year"
          v-model="state.newHouse.year" 
          class="form-control" 
          placeholder="Year Built..."
          required>
      </div>
      <div class="form-group">
        <label for="price">Price</label>
        <input 
          type="number" 
          name="price" 
          v-model="state.newHouse.price"
          class="form-control" 
          placeholder="Price..."
          required>
      </div>
      <div class="form-group">
        <label for="imgUrl">Image Url</label>
        <input 
          type="text" 
          name="imgUrl"
          v-model="state.newHouse.imgUrl"
          class="form-control" 
          placeholder="Url...">
      </div>
      <div class="form-group">
        <label for="description">Description</label>
        <input 
          type="text" 
          name="description"
          v-model="state.newHouse.description" 
          class="form-control"
          placeholder="Description..." maxlength="240">
        </div>
        <div class="d-flex align-items-center">
          <button type="submit" class="btn btn-outline-success my-2 mx-2 shadow">Add</button>
        </div>
      </form>
</div>
</template>

<script>
import { reactive } from '@vue/reactivity'
import { housesService } from '../services/HousesService'
import { useRouter } from 'vue-router'
export default {
  setup() {
    const router = useRouter()
    const state = reactive({
      newHouse: {}
    })
    return {
      state,
      async createHouse(){
        try {
          const newId = await housesService.createHouse(state.newHouse)
          state.newHouse = {}
          router.push({name: 'HouseDetails', params: {id: newId}})
        } catch (error) {
          console.error(error)
        }
      }
    }
  }
}
</script>


<style>
</style>
        