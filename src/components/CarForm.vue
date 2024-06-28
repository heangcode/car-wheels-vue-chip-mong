<template>
  <div class="mb-4">
    <form @submit.prevent="handleSubmit">
      <label class="block mb-2">Car Name:</label>
      <input
        v-model="name"
        class="border p-2 w-full mb-4"
        type="text"
        required
      />

      <label class="block mb-2">Number of Wheels:</label>
      <input
        v-model.number="wheels"
        class="border p-2 w-full mb-4"
        type="number"
        required
      />

      <button class="bg-blue-500 text-white px-4 py-2" type="submit">
        Add Car
      </button>
    </form>
    <div v-if="errorMessage" class="mt-4 text-red-500">{{ errorMessage }}</div>
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
