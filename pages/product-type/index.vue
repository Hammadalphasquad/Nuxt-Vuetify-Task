<template>
  <v-container>
    <v-row>
      <v-col>
        <p class="text-h2 font-weight-bold border-b-2 py-8 pl-5 border-primary text-primary">
          Product Type
        </p>
      </v-col>
    </v-row>

    <v-row class="pl-5 pt-5">
      <v-col cols="12" md="3">
        <p class="text-body-1 font-medium text-gray-800 mb-6">
          Product type per category
        </p>

        <v-list dense>
          <v-list-item
            v-for="(tab, index) in tabs"
            :key="index"
            @click="activateTab(index)"
            :class="{ 'primary--text': activeTab === index }"
          >
            <v-list-item-title>{{ tab.label }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-col>

      <!-- Display active tab content -->
      <v-col cols="12" md="9">
        <div v-if="activeTab === 0">
          <slot name="tab1">
            <PrintOnly />
          </slot>
        </div>
        <div v-else-if="activeTab === 1">
          <slot name="tab2">
            <PrintMail />
          </slot>
        </div>
        <div v-else-if="activeTab === 2">
          <slot name="tab3">
            <Electronic />
          </slot>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      activeTab: 0, // Index of the initially active tab
      tabs: [
        { label: 'Print Only', name: 'tab1' },
        { label: 'Print and Mail', name: 'tab2' },
        { label: 'Electronic', name: 'tab3' },
      ],
    };
  },
  methods: {
    activateTab(index) {
      this.activeTab = index;
    },
  },
};
</script>