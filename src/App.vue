<template>
  <div class="container mx-auto p-4 w-full">
    <div class="flex items-start w-full space-x-10">
      <div class="flex flex-col w-full">
        <h1 class="text-3xl font-bold mb-6 text-center">
          Car Wheel Information
        </h1>
        <QueryForm @query="handleQuery" @bye="openByeModal" />
        <CarForm :cars="cars" @new-car="addCar" />
      </div>
      <div class="w-full">
        <CarList :cars="displayedCars" />
      </div>
    </div>
    <ByeModal
      v-if="isByeModalOpen"
      @confirm="closeProgram"
      @cancel="closeByeModal"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import CarForm from "./components/CarForm.vue";
import QueryForm from "./components/QueryForm.vue";
import CarList from "./components/CarList.vue";
import ByeModal from "./components/ByeModal.vue";

interface Car {
  name: string;
  wheels: number;
}

export default defineComponent({
  name: "App",
  components: {
    CarForm,
    QueryForm,
    CarList,
    ByeModal,
  },
  setup() {
    const cars = ref<Car[]>([]);
    const displayedCars = ref<Car[]>([]);
    const isByeModalOpen = ref(false);

    const addCar = (car: Car) => {
      cars.value.push(car);
      displayedCars.value = cars.value;
    };

    const handleQuery = (query: string) => {
      if (query.toLowerCase() === "all") {
        displayedCars.value = cars.value;
      } else if (query.toLowerCase() === "2-wheel-car") {
        displayedCars.value = cars.value.filter((car) => car.wheels === 2);
      } else if (query.toLowerCase() === "4-wheel-car") {
        displayedCars.value = cars.value.filter((car) => car.wheels === 4);
      }
    };

    const openByeModal = () => {
      isByeModalOpen.value = true;
    };

    const closeByeModal = () => {
      isByeModalOpen.value = false;
    };

    const closeProgram = () => {
      alert("Closing the application.");
      isByeModalOpen.value = false;
    };

    return {
      cars,
      displayedCars,
      isByeModalOpen,
      addCar,
      handleQuery,
      openByeModal,
      closeByeModal,
      closeProgram,
    };
  },
});
</script>
