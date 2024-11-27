<script setup>
const slides = [
  {
    id: 1,
    title: '1. Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur\nsed do eiusmod tempor incididunt ut\nlabore et dolore magna aliqua.',
    image: '/images/main.jpg'
  },
  {
    id: 2,
    title: '2.Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur\nsed do eiusmod tempor incididunt ut\nlabore et dolore magna aliqua.',
    image: '/images/main.jpg'
  },
  {
    id: 3,
    title: '3.Lorem ipsum\ndolor sit amet,',
    description: 'Lorem ipsum dolor sit amet, consectetur\nsed do eiusmod tempor incididunt ut\nlabore et dolore magna aliqua.',
    image: '/images/main.jpg'
  }
]

const extendedSlides = computed(() => [
  { ...slides[slides.length - 1], id: 'clone-last' },
  ...slides,
  { ...slides[0], id: 'clone-first' }
])

const currentSlide = ref(1)
const containerRef = ref(null)
const slideWidth = ref(0)

const SLIDE_WIDTH = 1920
const SLIDE_HEIGHT = 740

const updateSlideWidth = () => {
  slideWidth.value = Math.min(window.innerWidth, SLIDE_WIDTH)
}

onMounted(() => {
  updateSlideWidth()
  window.addEventListener('resize', updateSlideWidth)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateSlideWidth)
})

const moveSlide = (direction) => {
  const container = containerRef.value
  if (!container) return
  
  container.style.transition = 'transform 0.5s'
  
  if (direction === 'next') {
    currentSlide.value++
  } else {
    currentSlide.value--
  }
}

const handleTransitionEnd = () => {
  const container = containerRef.value
  if (!container) return

  if (currentSlide.value >= slides.length + 1) {
    container.style.transition = 'none'
    currentSlide.value = 1
  } else if (currentSlide.value <= 0) {
    container.style.transition = 'none'
    currentSlide.value = slides.length
  }
}
</script>

<template>
  <button 
    @click="moveSlide('prev')"
    class="absolute left-3 sm:left-5 md:left-8 lg:left-12 top-1/2 -translate-y-1/2 flex items-center justify-center text-white z-10 hover:opacity-70 duration-300"
  >
    <span class="sr-only">이전</span>
    <NuxtImg 
      src="/images/arrow-left.svg" 
      alt="이전" 
      class="w-5 sm:w-6 md:w-8 lg:w-10"
    />
  </button>
  <button 
    @click="moveSlide('next')"
    class="absolute right-3 sm:right-5 md:right-8 lg:right-12 top-1/2 -translate-y-1/2 flex items-center justify-center text-white z-10 hover:opacity-70 duration-300"
  >
    <span class="sr-only">다음</span>
    <NuxtImg 
      src="/images/arrow-right.svg" 
      alt="다음" 
      class="w-5 sm:w-6 md:w-8 lg:w-10"
    />
  </button>
  <section class="relative h-[500px] sm:h-[600px] md:h-[680px] lg:h-[740px] w-full overflow-hidden">
    <div
      ref="containerRef"
      class="absolute inset-0 flex h-full"
      :style="{
        transform: `translateX(-${currentSlide * slideWidth}px)`,
        width: `${extendedSlides.length * slideWidth}px`
      }"
      @transitionend="handleTransitionEnd"
    >
      <div 
        v-for="(slide, index) in extendedSlides" 
        :key="slide.id"
        :style="{ width: `${slideWidth}px` }"
        class="h-full flex-shrink-0"
      >
        <div
          class="relative w-full h-full max-w-[1920px] mx-auto bg-cover bg-center"
          :style="{ 
            backgroundImage: `url(${slide.image})`,
            backgroundSize: 'cover',
            backgroundPosition: 'center'
          }"
        >
          <div class="absolute inset-0 bg-black/40"></div>
          <div class="container relative h-full mx-auto flex items-center">
            <div class="text-white max-w-[260px] sm:max-w-[320px] md:max-w-[600px] lg:max-w-[800px] px-4 sm:px-6 md:px-8 lg:px-0">
              <h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-black mb-3 sm:mb-4 md:mb-6 lg:mb-8 leading-tight whitespace-pre-line">
                {{ slide.title }}
              </h1>
              <p class="text-sm sm:text-base md:text-lg lg:text-xl leading-relaxed whitespace-pre-line">
                {{ slide.description }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>