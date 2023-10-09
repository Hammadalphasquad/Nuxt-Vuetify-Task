<template>
  <v-container>
    <v-row>
      <v-col>
        <p class="text-h2 font-weight-bold border-b-2 py-8 pl-5 border-primary text-primary">
          Categories
        </p>
      </v-col>
    </v-row>
    
    <!-- Content -->
    <v-row class="gap-4">
      <v-col class="pl-5 pt-5 max-w-md">
        <p class="text-body-1 font-medium text-gray-800 mb-6">Categories</p>
        <!-- Inputs -->
        <v-form>
          <v-row v-for="(input, index) in inputs" :key="index">
            <v-col cols="12" sm="6" md="4">
              <v-text-field
                v-model="input.value"
                :label="'Input ' + (index + 1)"
                outlined
                class="mb-6"
              ></v-text-field>
            </v-col>
            <!-- Cross Icon -->
            <v-col v-if="index > 0">
              <v-icon
                class="cursor-pointer"
                @click="removeInput(index)"
                color="primary"
              >
                mdi-close
              </v-icon>
            </v-col>
          </v-row>
          <!-- Add Button -->
          <v-row>
            <v-col>
              <v-btn
                @click="addInput"
                color="primary"
                text
                class="mb-4"
              >
                <v-icon left>mdi-plus</v-icon>Add Input
              </v-btn>
            </v-col>
          </v-row>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const inputs = ref([
  { value: "Print Only" },
  { value: "Print and Mail" },
  { value: "Electronic" },
]);

const addInput = () => {
  inputs.value.push({ value: "" });
};

const removeInput = (index) => {
  inputs.value.splice(index, 1);
};
</script>