<template>
    <button
      :class="[ 
        'flex items-center justify-center font-semibold rounded-lg shadow-md transition duration-300 ease-in-out',
        sizeClass,
        colorClass,
        icon ? 'space-x-2' : ''
      ]"
      @click="handleClick"
    >
      
      <span v-if="icon" class="icon">
        <i :class="icon"></i>
      </span>
  
      
      <span>{{ label }}</span>
    </button>
  </template>
  
  <script>
  export default {
    props: {
      label: {
        type: String,
        required: true,
      },
      color: {
        type: String,
        default: 'blue',
      },
      size: {
        type: String,
        default: 'medium',
      },
      icon: {
        type: String,
        default: null,
      },
    },
    computed: {
      colorClass() {
        const colors = {
          red: 'bg-red-500 text-white hover:bg-red-600',
          blue: 'bg-blue-500 text-white hover:bg-blue-600',
          green: 'bg-green-500 text-white hover:bg-green-600',
          yellow: 'bg-yellow-500 text-black hover:bg-yellow-600',
          gray: 'bg-gray-500 text-white hover:bg-gray-600',
        };
        return colors[this.color] || colors.blue;
      },
      sizeClass() {
        const sizes = {
          small: 'px-3 py-1 text-xs',
          medium: 'px-4 py-2 text-base',
          large: 'px-6 py-3 text-lg',
        };
        return sizes[this.size] || sizes.medium;
      },
    },
    methods: {
      handleClick() {
        
        this.$emit('click');
      },
    },
  };
  </script>
  
  <style scoped>
  .icon {
    display: flex;
    align-items: center;
  }
  </style>
  