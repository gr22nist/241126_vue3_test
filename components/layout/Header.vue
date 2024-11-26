<script setup>
import Logo from '../common/Logo.vue'

const menuItems = [
  { id: 1, name: 'Home', key: 'Home' },
  { id: 2, name: 'About', key: 'About' },
  { id: 3, name: 'Contact', key: 'Contact' }
]

const handleMenuClick = (menuName) => {
  console.log(`${menuName} 클릭`)
}
</script>

<template>
  <header class="bg-white shadow">
    <nav class="container max-w-8xl mx-auto py-2">
      <div class="flex justify-between items-center">
        <div class="flex items-center">
          <Logo class="text-[#140700]" />
        </div>
        <ul class="flex gap-10">
          <li v-for="item in menuItems" :key="item.id">
            <a href="#" 
               @click.prevent="handleMenuClick(item.key)" 
               class="font-bold uppercase hover:text-blue-500">
               {{ item.name }}
            </a>
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>
