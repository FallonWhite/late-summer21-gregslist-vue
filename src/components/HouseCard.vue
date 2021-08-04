<template>
      <div class="house m-2 bg-light shadow">
        <router-link :to="{name: 'HouseDetails', params: {id: house.id}}">
          <img :src="house.imgUrl" class="w-100">
          <div class="p-3">
              <div class="text-center">
                {{ house.price }}<br />
                {{ house.bedrooms }} Bedrooms, - {{ house.bathrooms }} Bathrooms<br />
                Built {{ house.year }}, Levels {{ house.levels }}<br />
              </div>
              <p>{{house.description}}</p>
              <p><em>{{house.price}}</em></p>
          </div>
        </router-link>
      </div>
</template>

<script>
export default {
  props: {
    car: {
      type: Object,
      required: true
    },
    house: {
      type: Object,
      required: true
    }
  },
  setup(){
    return {}
  }}
</script>


<style>
</style>