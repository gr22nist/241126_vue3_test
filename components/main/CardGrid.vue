<script setup>
const cards = [
  {
    id: 1,
    image: '/images/img1.jpg',
    title: 'Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    tags: ['Lorem ipsum dolor sit amet,']
  },
  {
    id: 2,
    image: '/images/img2.jpg',
    title: 'Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    tags: ['Lorem ipsum dolor sit amet,']
  },
  {
    id: 3,
    image: '/images/img3.jpg',
    title: 'Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    tags: ['Lorem ipsum dolor sit amet,']
  },
  {
    id: 4,
    image: '/images/img4.jpg',
    title: 'Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    tags: ['Lorem ipsum dolor sit amet,']
  },
]
</script>

<template>
  <section class="py-40">
    <div class="container mx-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <article 
          v-for="card in cards" 
          :key="card.id"
          class="bg-white rounded-lg shadow-xl overflow-hidden flex flex-col"
        >
          <div class="aspect-w-16 aspect-h-9">
            <img 
              :src="card.image"
              :alt="card.title"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="h-[250px] xl:h-[290px] p-7 flex-grow flex flex-col gap-5">
            <h3 class="text-2xl xl:text-3xl font-black leading-tight whitespace-pre-line">{{ card.title }}</h3>
            <p class="text-gray-600 mb-4 flex-grow">{{ card.description }}</p>
            <div class="flex flex-wrap gap-2">
              <span 
                v-for="tag in card.tags" 
                :key="tag"
                class="text-sm text-gray-300"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>