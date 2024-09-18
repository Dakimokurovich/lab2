<template>
    <div class="space-y-4">
      <h2 class="text-xl font-bold">Button Component Demo</h2>
      <Button label="Red Button" color="red" size="large" @click="handleButtonClick" />
      <Button label="Blue Button" color="blue" size="medium" icon="⭐" @click="handleButtonClick" />
  
      <h2 class="text-xl font-bold">SearchableDropdown Demo</h2>
      <SearchableDropdown :items="dropdownItems" @select="handleSelect" />
    </div>
  </template>
  
  <script>
  import Button from '../components/Button.vue';
  import SearchableDropdown from '../components/SearchableDropdown.vue';
  
  export default {
    components: {
      Button,
      SearchableDropdown,
    },
    data() {
      return {
        dropdownItems: ['Apple', 'Banana', 'Cherry', 'Date', 'Fig', 'Grape'],
      };
    },
    methods: {
      handleButtonClick() {
        alert('Button clicked!');
      },
      handleSelect(item) {
        alert(`Selected: ${item}`);
      },
    },
  };
  </script>
  