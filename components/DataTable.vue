<template>
  <div class="flex flex-col gap-4 max-w-[1124px] w-full mx-auto max-h-[409px] h-full mt-[37px]">
    <div class="flex w-full justify-end">
      <!-- Add New Button -->
      <v-btn @click="addNewRow" color="primary" class="text-base font-bold"> Add new </v-btn>
    </div>
    <div class="border-[1px] border-[e5e7eb] rounded-md">
      <div class="overflow-x-auto">
        <table class="min-w-full bg-white font-[sans-serif]">
          <thead class="bg-[#D9D9D9] whitespace-nowrap">
            <tr>
              <th class="px-6 py-[22px] text-left text-base font-bold text-slate-600 leading-4">
                ID
              </th>
              <th class="px-6 py-[22px] text-left text-base font-bold text-slate-600 leading-4">
                Size Name
              </th>
              <th
                class="px-6 py-[22px] text-left text-base font-bold text-slate-600 flex w-full justify-end"
              >
                Actions
              </th>
            </tr>
          </thead>
          <tbody class="whitespace-nowrap">
            <tr class="hover:bg-gray-50" v-for="(item, index) in sizeData" :key="index">
              <td class="px-6 py-[27px] text-sm font-normal leading-[14px] text-gray-600">
                {{ item.id }}
              </td>
              <td class="px-6 py-[27px] text-sm font-normal leading-[14px] text-gray-600">
                <span v-if="!item.isEditing">{{ item.sizeName }}</span>
                <input v-else v-model="item.editedSizeName" type="text" class="border p-2 w-full" />
              </td>
              <td class="px-6 py-[27px]">
                <div class="flex w-full justify-end ml-4">
                  <button @click="toggleEdit(index)" class="mr-4" title="Edit">
                    <!-- ... Edit Icon ... -->
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      class="w-5 fill-blue-500 hover:fill-blue-700"
                      viewBox="0 0 348.882 348.882"
                    >
                      <path
                        d="m333.988 11.758-.42-.383A43.363 43.363 0 0 0 304.258 0a43.579 43.579 0 0 0-32.104 14.153L116.803 184.231a14.993 14.993 0 0 0-3.154 5.37l-18.267 54.762c-2.112 6.331-1.052 13.333 2.835 18.729 3.918 5.438 10.23 8.685 16.886 8.685h.001c2.879 0 5.693-.592 8.362-1.76l52.89-23.138a14.985 14.985 0 0 0 5.063-3.626L336.771 73.176c16.166-17.697 14.919-45.247-2.783-61.418zM130.381 234.247l10.719-32.134.904-.99 20.316 18.556-.904.99-31.035 13.578zm184.24-181.304L182.553 197.53l-20.316-18.556L294.305 34.386c2.583-2.828 6.118-4.386 9.954-4.386 3.365 0 6.588 1.252 9.082 3.53l.419.383c5.484 5.009 5.87 13.546.861 19.03z"
                        data-original="#000000"
                      />
                      <path
                        d="M303.85 138.388c-8.284 0-15 6.716-15 15v127.347c0 21.034-17.113 38.147-38.147 38.147H68.904c-21.035 0-38.147-17.113-38.147-38.147V100.413c0-21.034 17.113-38.147 38.147-38.147h131.587c8.284 0 15-6.716 15-15s-6.716-15-15-15H68.904C31.327 32.266.757 62.837.757 100.413v180.321c0 37.576 30.571 68.147 68.147 68.147h181.798c37.576 0 68.147-30.571 68.147-68.147V153.388c.001-8.284-6.715-15-14.999-15z"
                        data-original="#000000"
                      />
                    </svg>
                  </button>
                  <button @click="deleteItem(index)" class="mr-4" title="Delete">
                    <!-- ... Delete Icon ... -->
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      class="w-5 fill-red-500 hover:fill-red-700"
                      viewBox="0 0 24 24"
                    >
                      <path
                        d="M19 7a1 1 0 0 0-1 1v11.191A1.92 1.92 0 0 1 15.99 21H8.01A1.92 1.92 0 0 1 6 19.191V8a1 1 0 0 0-2 0v11.191A3.918 3.918 0 0 0 8.01 23h7.98A3.918 3.918 0 0 0 20 19.191V8a1 1 0 0 0-1-1Zm1-3h-4V2a1 1 0 0 0-1-1H9a1 1 0 0 0-1 1v2H4a1 1 0 0 0 0 2h16a1 1 0 0 0 0-2ZM10 4V3h4v1Z"
                        data-original="#000000"
                      />
                      <path
                        d="M11 17v-7a1 1 0 0 0-2 0v7a1 1 0 0 0 2 0Zm4 0v-7a1 1 0 0 0-2 0v7a1 1 0 0 0 2 0Z"
                        data-original="#000000"
                      />
                    </svg>
                  </button>
                  <button @click="saveEdit(index)" class="mr-4" title="Save" v-if="item.isEditing">
                    <!-- ... Save Icon ... -->
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      height="1.3em"
                      fill="darkgreen"
                      viewBox="0 0 448 512"
                    >
                      <path
                        d="M48 96V416c0 8.8 7.2 16 16 16H384c8.8 0 16-7.2 16-16V170.5c0-4.2-1.7-8.3-4.7-11.3l33.9-33.9c12 12 18.7 28.3 18.7 45.3V416c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V96C0 60.7 28.7 32 64 32H309.5c17 0 33.3 6.7 45.3 18.7l74.5 74.5-33.9 33.9L320.8 84.7c-.3-.3-.5-.5-.8-.8V184c0 13.3-10.7 24-24 24H104c-13.3 0-24-10.7-24-24V80H64c-8.8 0-16 7.2-16 16zm80-16v80H272V80H128zm32 240a64 64 0 1 1 128 0 64 64 0 1 1 -128 0z"
                      />
                    </svg>
                  </button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sizeData: [
        { id: 124124, sizeName: "11 x 8.5 One sided", isEditing: false, editedSizeName: "" },
        { id: 125215, sizeName: "11 x 8.5 Two sided", isEditing: false, editedSizeName: "" },
        { id: 125125, sizeName: "6.5 x 8", isEditing: false, editedSizeName: "" },
        // Add more data as needed
      ],
    };
  },
  methods: {
    addNewRow() {
      // Add a new row with a unique ID and default values
      const newItem = {
        id: Date.now(),
        sizeName: "New Size Name",
        isEditing: false,
        editedSizeName: "",
      };
      this.sizeData.push(newItem);
    },
    toggleEdit(index) {
      // Toggle the editing state
      this.sizeData[index].isEditing = !this.sizeData[index].isEditing;
      // If editing is enabled, set the editedSizeName to the current sizeName
      if (this.sizeData[index].isEditing) {
        this.sizeData[index].editedSizeName = this.sizeData[index].sizeName;
      }
    },
    saveEdit(index) {
      // Save the edited sizeName and disable editing
      this.sizeData[index].sizeName = this.sizeData[index].editedSizeName;
      this.sizeData[index].isEditing = false;
    },
    deleteItem(index) {
      // Implement your delete functionality here using the index
      this.sizeData.splice(index, 1);
    },
  },
};
</script>
