<template>
  <v-row>
    <v-col cols="12" md="6">
      <v-card>
        <v-card-title>Inputs</v-card-title>
        <v-card-text>
          <v-form>
            <v-row v-for="(input, index) in inputs" :key="index" align="center">
              <v-col cols="10">
                <v-text-field
                
                  v-model="input.value"
                  :label="'Input ' + (index + 1)"
                  outlined
                  dense
                ></v-text-field>
              </v-col>
              <v-col cols="2">
                <v-icon
                color="primary"
                  v-if="index > 0"
                  @click="removeInput(index)"
                  class="cursor-pointer"
                >
                  mdi-close
                </v-icon>
              </v-col>
            </v-row>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn @click="addInput" color="primary">Add Input</v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script setup>
import { ref } from "vue";

const inputs = ref([
  { value: "Postcards" },
  { value: "Business Cards" },
]);

const addInput = () => {
  inputs.value.push({ value: "" });
};

const removeInput = (index) => {
  inputs.value.splice(index, 1);
};
</script>