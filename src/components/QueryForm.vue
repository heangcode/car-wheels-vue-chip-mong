<template>
  <div class="mb-4 w-full">
    <form @submit.prevent="handleQuery" class="w-full">
      <label
        for="query-search"
        class="mb-4 text-md font-medium text-gray-900 sr-only"
        >Search</label
      >
      <div class="relative">
        <div
          class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
        >
          <svg
            class="w-4 h-4 text-gray-500"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 20 20"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
            />
          </svg>
        </div>
        <input
          v-model="query"
          id="query-search"
          type="search"
          class="block w-full p-3 ps-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500"
          placeholder="Enter your query (e.g., 4-wheel-car, 2-wheel-car, All, Bye...)"
          required
        />
        <button
          type="submit"
          class="text-white absolute end-2.5 bottom-1.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Search
        </button>
      </div>
    </form>
    <div class="flex flex-wrap gap-2 mt-4">
      <div
        v-for="suggestion in suggestions"
        :key="suggestion"
        @click="toggleQuery(suggestion)"
        :class="[
          'px-4 py-2 rounded-full focus:outline-none flex items-center space-x-2 cursor-pointer',
          query === suggestion
            ? 'bg-blue-200 text-blue-700'
            : 'bg-gray-200 text-gray-700 hover:bg-gray-300',
        ]"
      >
        <span>{{ suggestion }}</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "QueryForm",
  emits: ["query", "bye"],
  setup(_, { emit }) {
    const query = ref("");
    const suggestions = ref(["4-wheel-car", "2-wheel-car", "All", "Bye"]);

    const handleQuery = () => {
      if (query.value === "Bye") {
        emit("bye");
      } else {
        emit("query", query.value);
      }
    };

    const toggleQuery = (suggestion: string) => {
      if (query.value === suggestion) {
        query.value = "";
      } else {
        query.value = suggestion;
        handleQuery();
      }
    };

    return {
      query,
      suggestions,
      handleQuery,
      toggleQuery,
    };
  },
});
</script>
