<template>
    <div class="relative">
      <input
        type="text"
        v-model="searchTerm"
        @focus="isOpen = true"
        @keydown.down.prevent="moveDown"
        @keydown.up.prevent="moveUp"
        @keydown.enter.prevent="selectHighlighted"
        @blur="closeDropdown"
        class="px-4 py-2 border rounded-lg w-full"
        placeholder="Search..."
      />
      <button
        v-if="selectedItems.length > 0"
        @click="clearSelection"
        class="absolute right-2 top-2 text-gray-500 hover:text-gray-700"
      >
        Очистити
      </button>
  
      <ul
        v-if="isOpen"
        class="absolute left-0 w-full mt-2 bg-white border rounded-lg max-h-48 overflow-y-auto z-10"
      >
        <li
          v-for="(item, index) in filteredItems"
          :key="item"
          @click="selectItem(item)"
          :class="[
            'px-4 py-2 cursor-pointer hover:bg-gray-200',
            index === highlightedIndex ? 'bg-gray-200' : '',
          ]"
        >
          {{ item }}
        </li>
        <li v-if="filteredItems.length === 0" class="px-4 py-2 text-gray-500">
          Нічого не знайдено
        </li>
      </ul>
  
      <div v-if="selectedItems.length > 0" class="mt-2 space-x-2">
        <span
          v-for="item in selectedItems"
          :key="item"
          class="inline-block bg-blue-500 text-white px-2 py-1 rounded"
        >
          {{ item }}
        </span>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      items: {
        type: Array,
        required: true,
      },
      multiple: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        searchTerm: '',
        isOpen: false,
        selectedItems: [],
        highlightedIndex: 0,
      };
    },
    computed: {
      filteredItems() {
        return this.items.filter((item) =>
          item.toLowerCase().includes(this.searchTerm.toLowerCase())
        );
      },
    },
    methods: {
      selectItem(item) {
        if (this.multiple) {
          if (!this.selectedItems.includes(item)) {
            this.selectedItems.push(item);
          }
        } else {
          this.selectedItems = [item];
        }
        this.$emit('select', this.selectedItems);
        this.searchTerm = this.multiple ? '' : item;
        this.isOpen = !this.multiple;
      },
      selectHighlighted() {
        if (this.filteredItems.length > 0) {
          this.selectItem(this.filteredItems[this.highlightedIndex]);
        }
      },
      moveDown() {
        if (this.highlightedIndex < this.filteredItems.length - 1) {
          this.highlightedIndex++;
        }
      },
      moveUp() {
        if (this.highlightedIndex > 0) {
          this.highlightedIndex--;
        }
      },
      closeDropdown() {
        setTimeout(() => {
          this.isOpen = false;
        }, 200);
      },
      clearSelection() {
        this.selectedItems = [];
        this.searchTerm = '';
        this.$emit('clear');
      },
    },
  };
  </script>
  
  <style scoped>
  
  </style>
  