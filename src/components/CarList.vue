<template>
  <div>
    <h2 class="text-xl font-bold mb-2">Registered Cars:</h2>
    <ul>
      <li v-for="car in cars" :key="car.name" class="mb-2">
        {{ car.name }} - {{ car.wheels }} wheels
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
  name: "CarList",
  props: {
    cars: {
      type: Array as PropType<{ name: string; wheels: number }[]>,
      required: true,
    },
  },
});
</script>
