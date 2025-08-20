<template>
  <div class="p-6">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-3xl font-bold text-gray-800">Список пользователей</h2>
      <div class="flex gap-3">
        <button
          @click="toggleListDisplay"
          class="px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition-colors duration-200"
        >
          {{ showList ? "Скрыть список" : "Показать список" }}
        </button>
        <button
          v-if="showList"
          @click="toggleAgeDisplay"
          class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors duration-200"
        >
          {{ showAge ? "Скрыть возраст" : "Показать возраст" }}
        </button>
      </div>
    </div>
    <div
      v-if="showList"
      class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"
    >
      <div
        v-for="user in users"
        :key="user.id"
        class="bg-white rounded-lg shadow-md hover:shadow-lg transition-all duration-200 hover:-translate-y-1 p-6 border border-gray-200 cursor-pointer"
        @mouseenter="hoveredUser = user.id"
        @mouseleave="hoveredUser = null"
      >
        <img
          :src="user.avatar"
          :alt="user.firstName"
          class="w-20 h-20 rounded-full object-cover mx-auto mb-4 shadow-md"
        />
        <div class="text-center">
          <h3
            :class="[
              hoveredUser === user.id ? 'text-blue-600' : 'text-gray-800',
            ]"
            class="text-lg font-semibold mb-2"
          >
            {{ user.firstName }}&nbsp;{{ user.lastName }}
          </h3>
          <p class="text-sm text-gray-600 mb-1">{{ user.email }}</p>
          <p v-if="showAge" class="text-sm text-gray-500">
            Возраст: {{ user.age }} лет
          </p>
        </div>
      </div>
    </div>
    <div v-else class="grid grid-cols-1">
      <div
        class="bg-white rounded-lg shadow-md hover:shadow-lg transition-all duration-200 hover:-translate-y-1 p-6 border border-gray-200 cursor-pointer"
      >
        <h3 class="text-lg font-semibold text-gray-800 mb-2">
          Список пользователей скрыт
        </h3>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { users } from "@/data/users.js";

const showAge = ref(true);
const showList = ref(true);
const hoveredUser = ref(null);

const toggleAgeDisplay = () => {
  showAge.value = !showAge.value;
};

const toggleListDisplay = () => {
  showList.value = !showList.value;
};
</script>
