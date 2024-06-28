<template>
  <div class="mb-4 w-full bg-white shadow-md rounded-lg p-6">
    <form @submit.prevent="handleSubmit">
      <div class="mb-4">
        <label class="block mb-2 font-semibold">Car Name:</label>
        <input
          v-model="name"
          class="border p-3 w-full mb-2 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
          type="text"
          placeholder="Enter car name"
          required
        />
      </div>

      <div class="mb-4">
        <label class="block mb-2 font-semibold">Number of Wheels:</label>
        <input
          v-model.number="wheels"
          class="border p-3 w-full mb-2 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
          type="number"
          min="1"
          placeholder="Enter number of wheels"
          required
        />
      </div>

      <button
        class="bg-blue-500 rounded-lg text-white px-4 py-2 hover:bg-blue-600 transition duration-200"
        type="submit"
      >
        Add Car
      </button>
    </form>
    <div v-if="errorMessage" class="mt-4 text-red-500 font-semibold">
      {{ errorMessage }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, PropType } from "vue";

export default defineComponent({
  name: "CarForm",
  props: {
    cars: {
      type: Array as PropType<{ name: string; wheels: number }[]>,
      required: true,
    },
  },
  emits: ["new-car"],
  setup(props, { emit }) {
    const name = ref("");
    const wheels = ref(4);
    const errorMessage = ref("");

    const handleSubmit = () => {
      const existingCar = props.cars.find(
        (car) => car.name.toLowerCase() === name.value.toLowerCase()
      );
      if (existingCar) {
        errorMessage.value = `"${name.value}" is already in the list.`;
      } else {
        emit("new-car", { name: name.value, wheels: wheels.value });
        name.value = "";
        wheels.value = 4;
        errorMessage.value = "";
      }
    };

    return {
      name,
      wheels,
      errorMessage,
      handleSubmit,
    };
  },
});
</script>
