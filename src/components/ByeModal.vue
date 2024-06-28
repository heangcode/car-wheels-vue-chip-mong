<template>
  <div
    class="fixed inset-0 bg-gray-500 bg-opacity-75 flex items-center justify-center"
  >
    <div class="bg-white p-6 rounded shadow-lg">
      <h2 class="text-lg font-bold mb-4">Are you sure you want to exit?</h2>
      <div class="flex justify-end">
        <button
          @click="cancel"
          class="bg-gray-300 text-black px-4 py-2 mr-2 rounded hover:bg-gray-400 transition duration-200"
        >
          Cancel
        </button>
        <button
          @click="confirm"
          class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-600 transition duration-200"
        >
          Exit
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ByeModal",
  emits: ["confirm", "cancel"],
  setup(_, { emit }) {
    const confirm = () => {
      emit("confirm");
    };

    const cancel = () => {
      emit("cancel");
    };

    return {
      confirm,
      cancel,
    };
  },
});
</script>
