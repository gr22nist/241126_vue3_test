<script setup>
const cards = [
  {
    id: 1,
    title: 'Title 1',
    subtitle: 'Category',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.',
    image: '/images/img1.jpg',
    date: '2024.11.27',
    tags: ['Design', 'Development']
  },
  {
    id: 2,
    title: 'Title 2',
    subtitle: 'Category',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    image: '/images/img2.jpg',
    date: '2024.11.27'
  },
  {
    id: 3,
    title: 'Title 3',
    subtitle: 'Category',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    image: '/images/img3.jpg',
    date: '2024.11.27'
  },
  {
    id: 4,
    title: 'Title 4',
    subtitle: 'Category',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    image: '/images/img4.jpg',
    date: '2024.11.27'
  },
]

const containerRef = ref(null)
const currentIndex = ref(0)

const goToSlide = (index) => {
  currentIndex.value = index
}
</script>

<template>
  <section class="relative bg-gray-100 h-[800px] flex items-center">
    <div class="container mx-auto px-4">
      <div ref="containerRef" class="overflow-hidden">
        <div
          class="flex transition-transform duration-700 ease-in-out"
          :style="{
            transform: `translateX(-${currentIndex * 100}%)`
          }"
        >
          <div 
            v-for="card in cards" 
            :key="card.id"
            class="w-full flex-shrink-0 flex"
          >
            <div class="mx-auto max-w-[1280px] flex flex-col lg:flex-row bg-white rounded-xl overflow-hidden">
              <div class="w-full lg:w-3/5 h-[300px] lg:h-[500px] relative">
                <img 
                  :src="card.image" 
                  :alt="card.title"
                  class="w-full h-full object-cover"
                />
              </div>
              <div class="w-full lg:w-2/5 p-6 lg:p-12 flex flex-col">
                <div class="space-y-4 lg:space-y-6">
                  <div class="flex justify-between items-center text-sm">
                    <span class="text-gray-500">{{ card.subtitle }}</span>
                    <span class="text-gray-400">{{ card.date }}</span>
                  </div>

                  <h3 class="text-2xl lg:text-3xl font-bold">
                    {{ card.title }}
                  </h3>

                  <p class="text-base text-gray-600 leading-relaxed line-clamp-3">
                    {{ card.description }}
                  </p>
                  <div class="flex flex-wrap gap-2">
                    <span 
                      v-for="tag in card.tags" 
                      :key="tag"
                      class="px-3 py-1 rounded-full bg-gray-100 text-gray-600 text-sm"
                    >
                      {{ tag }}
                    </span>
                  </div>

                  <button class="inline-flex items-center gap-2 text-gray-900 font-medium group mt-4">
                    Read More
                    <svg 
                      class="w-5 h-5 transform transition-transform group-hover:translate-x-1" 
                      fill="none" 
                      stroke="currentColor" 
                      viewBox="0 0 24 24"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                    </svg>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex gap-2">
        <button
          v-for="i in cards.length"
          :key="i"
          @click="goToSlide(i - 1)"
          class="w-2 h-2 rounded-full transition-all"
          :class="currentIndex === i - 1 ? 'bg-gray-800 w-4' : 'bg-gray-300'"
        >
          <span class="sr-only">프로젝트 {{ i }}</span>
        </button>
      </div>
    </div>
  </section>
</template>