<script setup>
import Logo from '../common/Logo.vue'
import { ref } from 'vue'

const menuItems = [
  { id: 1, name: 'Home', key: 'Home' },
  { id: 2, name: 'About', key: 'About' },
  { id: 3, name: 'Contact', key: 'Contact' }
]

const isMenuOpen = ref(false)

const handleMenuClick = (menuName) => {
  console.log(`${menuName} 클릭`)
  isMenuOpen.value = false
}

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
  console.log('메뉴 상태:', isMenuOpen.value)
}
</script>

<template>
  <header class="bg-white shadow relative z-50">
    <nav class="container mx-auto py-2 sm:py-3 md:py-4">
      <div class="flex justify-between items-center">
        <div class="flex items-center">
          <Logo 
            class="text-[#140700] scale-[0.5] sm:scale-[0.6] md:scale-[0.7] lg:scale-[0.8] origin-left" 
            width="252" 
            height="68"
          />
        </div>
        <button 
          class="md:hidden p-2 hover:bg-gray-100 rounded-lg"
          @click="toggleMenu"
        >
          <span class="sr-only">메뉴</span>
          <svg 
            xmlns="http://www.w3.org/2000/svg" 
            class="w-6 h-6" 
            fill="none" 
            viewBox="0 0 24 24" 
            stroke="currentColor"
          >
            <path 
              stroke-linecap="round" 
              stroke-linejoin="round" 
              stroke-width="2" 
              d="M4 6h16M4 12h16m-7 6h7" 
            />
          </svg>
        </button>
        <ul class="hidden md:flex gap-6 lg:gap-10">
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

    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div v-if="isMenuOpen" class="fixed inset-0 bg-black/50 z-40">
        <div class="fixed inset-y-0 right-0 w-64 bg-white shadow-lg">
          <div class="p-4 flex justify-between items-center border-b">
            <span class="font-bold">메뉴</span>
            <button 
              @click="toggleMenu"
              class="p-2 hover:bg-gray-100 rounded-lg"
            >
              <svg 
                xmlns="http://www.w3.org/2000/svg" 
                class="w-6 h-6" 
                fill="none" 
                viewBox="0 0 24 24" 
                stroke="currentColor"
              >
                <path 
                  stroke-linecap="round" 
                  stroke-linejoin="round" 
                  stroke-width="2" 
                  d="M6 18L18 6M6 6l12 12"
                />
              </svg>
            </button>
          </div>
          <ul class="py-2">
            <li v-for="item in menuItems" :key="item.id">
              <a 
                href="#" 
                @click.prevent="handleMenuClick(item.key)" 
                class="block px-4 py-2 font-bold uppercase hover:bg-gray-100"
              >
                {{ item.name }}
              </a>
            </li>
          </ul>
        </div>
      </div>
    </Transition>
  </header>
</template>
