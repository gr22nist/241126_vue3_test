<script setup>
import Logo from '../common/Logo.vue'

const slides = [
  {
    id: 1,
    title: '메인 타이틀 1',
    description: '첫 번째 슬라이드의 설명문구가 들어갑니다. 여러 줄의 텍스트가 들어갈 수 있습니다.',
    image: '/images/hero-1.jpg'
  },
  {
    id: 2,
    title: '메인 타이틀 2',
    description: '두 번째 슬라이드의 설명문구가 들어갑니다.',
    image: '/images/hero-2.jpg'
  }
]

const currentSlide = ref(0)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.length
}

const prevSlide = () => {
  currentSlide.value = currentSlide.value === 0 ? slides.length - 1 : currentSlide.value - 1
}
</script>

<template>
  <footer class="bg-[#1D1D1D] h-[250px] sm:h-[300px] md:h-[350px] flex items-center text-white">
    <div class="container mx-auto px-4 py-6">
      <div class="flex flex-col gap-8">
        <Logo 
          class="text-white scale-[0.7] sm:scale-[0.8] md:scale-100 origin-left" 
          accentColor="fill-white" 
          width="252" 
          height="68"
        />
        <div class="text-xs sm:text-sm">
          Copyrights 2024. <span class="font-bold">테스트</span> All rights Reserved.
        </div>
      </div>
    </div>
  </footer>
</template> 