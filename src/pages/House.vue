<template>
  <div class="house container-fluid">
    <div class="row">
      <div class="col">
        <HouseForm />
      </div>
    </div>
    <div class="row">
      <div class="col-4" v-for="h in houses" :key="h.id">
        <HouseCard :house="h" />
      </div>
    </div>
  </div>
</template>

<script>
import { computed, onMounted } from "@vue/runtime-core";
import { AppState } from "../AppState.js";
import { housesService } from "../services/HousesService";
import HouseCard from "../components/HouseCard.vue";
import HouseForm from "../components/HouseForm.vue";
export default {
  name: "House",
  setup() {
    onMounted(async () => {
      try {
        await housesService.getHouses();
      } catch (error) {
        console.error(error);
      }
    });
    return {
      houses: computed(() => AppState.houses),
    };
  },
  components: {
    HouseCard,
    HouseForm,
  },
};
</script>