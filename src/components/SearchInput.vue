<template>
  <form @submit.prevent>
    <div class="relative mt-6 flex justify-center items-center">
      <input
        type="text"
        v-model="searchText"
        placeholder="Search for movie...."
        autocomplete="email"
        aria-label="search"
        class="block w-80 rounded-2xl border border-neutral-300 bg-transparent py-4 pl-6 pr-20 text-base/6 text-neutral-950 ring-4 ring-transparent transition placeholder:text-neutral-500 focus:border-neutral-950 focus:outline-none focus:ring-neutral-950/5"
      />
      <div class="inset-y-1 flex justify-end">
        <button
        @click="$emit('sendText',searchText)"
          type="submit"
          aria-label="Submit"
          class="flex aspect-square h-full items-center justify-center rounded-xl mx-1 py-5 px-5 bg-slate-300 text-black transition hover:bg-slate-600"
        >
          <svg viewBox="0 0 16 6" aria-hidden="true" class="w-4">
            <path
              fill="currentColor"
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M16 3 10 .5v2H0v1h10v2L16 3Z"
            ></path>
          </svg>
        </button>
      </div>
    </div>
  </form>
</template>

<script setup>
import { ref } from "vue";
const searchText = ref("");
</script>
