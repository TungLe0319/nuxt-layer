<template>
  <UCard class=" "  :ui="{
    base: 'overflow-hidden hover:brightness-75 transition-all duration-150  ',
    background: '', // Change to your desired background color
    divide: '', // Adjust divide color
    ring: 'ring-1 ring-gray-300 dark:ring-gray-700', // Adjust ring color
    rounded: 'rounded-md', // Change to your desired border radius
    shadow: 'shadow-md', // Change to your desired shadow class
    body: {
      base: 'flex items-center justify-center flex-col space-y-5',
      background: '', // Change to your desired body background color
      padding: 'p-4', // Adjust padding
    },
    header: {
      base: '',
      background: 'bg-blue-500 text-white', // Change to your desired header background color and text color
      padding: 'px-4 py-5 sm:px-6',
    },
    footer: {
      base: '',
      background: 'bg-gray-200', // Change to your desired footer background color
      padding: 'px-4 py-4 sm:px-6',
    },
  }">
    <Icon :name="icon" class="" size="100" />

    <span class="text-3xl font-bold font-serif">
     {{ title }}
    </span>
     <span class="text-xl  font-sans">
       {{ content }}
      </span>
  </UCard>
</template>

<script lang="ts" setup>

const props = defineProps(['icon', 'title','content']);
</script>
