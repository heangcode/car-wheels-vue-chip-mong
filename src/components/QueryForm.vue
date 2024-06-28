<template>
  <div class="mb-4">
    <form @submit.prevent="handleQuery">
      <label class="block mb-2">Query:</label>
      <input
        v-model="query"
        class="border p-2 w-full mb-4"
        type="text"
        placeholder="4-wheel-car, 2-wheel-car, All, Bye"
        required
      />

      <button class="bg-green-500 text-white px-4 py-2" type="submit">
        Query
      </button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "QueryForm",
  emits: ["query", "bye"],
  setup(_, { emit }) {
    const query = ref("");

    const handleQuery = () => {
      if (query.value === "Bye") {
        emit("bye");
      } else {
        emit("query", query.value);
      }
      query.value = "";
    };

    return {
      query,
      handleQuery,
    };
  },
});
</script>
