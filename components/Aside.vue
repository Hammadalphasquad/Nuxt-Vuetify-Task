<template>
  <v-card class="max-w-[260px] w-full h-[833px] text-[#717D96] bg-[#EDF0F7]">
    <v-card-text>
      <div
      class="flex items-center py-3 hover:bg-[#E2E7F0] pl-10 gap-[10px] hover:text-[#2D3648] cursor-pointer"
    >
      <v-icon>
        mdi-cog
      </v-icon>
      <p class="text-sm leading-6 font-medium">Products</p>
      <i class="fa"></i>
    </div>
      <div
        @click="isSettingsOpen = !isSettingsOpen"
        class="flex items-center py-3 hover:bg-[#E2E7F0] pl-10 gap-[10px] hover:text-[#2D3648] cursor-pointer"
      >
        <v-icon>
          mdi-cog
        </v-icon>
        <p class="text-sm leading-6 font-medium">Settings</p>
        <i class="fa"></i>
      </div>
      <v-expand-transition>
        <div v-if="isSettingsOpen">
          <v-list dense>
            <v-list-item
              to="/categories"
              exact-active-class="bg-[#D4D8DF]"
              class="hover:bg-[#D4D8DF] cursor-pointer"
            >
              <v-list-item-title class="pl-[67px]">Categories</v-list-item-title>
            </v-list-item>
            <v-list-item
              to="/product-type"
              exact-active-class="bg-[#D4D8DF]"
              class="hover:bg-[#D4D8DF] cursor-pointer"
            >
              <v-list-item-title class="pl-[67px]">Product Type</v-list-item-title>
            </v-list-item>
            <v-list-item
              to="/product-size"
              exact-active-class="bg-[#D4D8DF]"
              class="hover:bg-[#D4D8DF] cursor-pointer"
            >
              <v-list-item-title class="pl-[67px]">Product Size</v-list-item-title>
            </v-list-item>
            <v-list-item
              
              exact-active-class="bg-[#D4D8DF]"
              class="hover:bg-[#D4D8DF] cursor-pointer"
            >
              <v-list-item-title class="pl-[67px]">Attributes</v-list-item-title>
            </v-list-item>
          </v-list>
        </div>
      </v-expand-transition>
    </v-card-text>
  </v-card>
</template>

<script setup>
import { ref } from 'vue';

const isSettingsOpen = ref(false);

const inputs = ref([
  { value: 'Print Only' },
  { value: 'Print and Mail' },
  { value: 'Electronic' },
]);

const addInput = () => {
  inputs.value.push({ value: '' });
};

const removeInput = (index) => {
  inputs.value.splice(index, 1);
};
</script>