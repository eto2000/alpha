<template>
    <div class="container">
      <div class="alphabet-list" ref="alphabetListRef" @scroll="handleScroll">
        <div v-for="item in alphabetData.alphabet" :key="item.letter" class="letter-section">
          <h2>{{ item.letter }}</h2>
          <swiper
            :slides-per-view="1"
            :space-between="30"
            :navigation="true"
            :modules="[navigation]"
            class="word-swiper"
          >
            <swiper-slide v-for="word in item.words" :key="word.word" class="word-card">
              <h3>{{ word.word }}</h3>
              <div class="spelling">
                <span v-for="(spell, index) in word.spelling" :key="index">
                  {{ spell }}
                </span>
              </div>
              <p class="pronunciation">발음: {{ word.pronunciation }}</p>
            </swiper-slide>
          </swiper>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { Swiper, SwiperSlide } from 'swiper/vue'
  import { Navigation } from 'swiper/modules'
  import 'swiper/css'
  import 'swiper/css/navigation'
  import alphabetData from './assets/alphabet-data.json'
  
  const navigation = Navigation
  const alphabetListRef = ref(null)
  let scrollTimeout = null
  
  // 스크롤 위치 저장 함수
  const handleScroll = () => {
    if (scrollTimeout) {
      clearTimeout(scrollTimeout)
    }
    
    scrollTimeout = setTimeout(() => {
      const sections = alphabetListRef.value.querySelectorAll('.letter-section')
      const scrollPosition = alphabetListRef.value.scrollTop
      const windowHeight = window.innerHeight
  
      // 현재 보이는 섹션 찾기
      let currentSection = null
      sections.forEach((section) => {
        const sectionTop = section.offsetTop
        const sectionBottom = sectionTop + section.offsetHeight
        
        if (scrollPosition >= sectionTop - windowHeight/2 && 
            scrollPosition < sectionBottom - windowHeight/2) {
          currentSection = section
        }
      })
  
      if (currentSection) {
        const letter = currentSection.querySelector('h2').textContent
        localStorage.setItem('lastLetter', letter)
      }
    }, 100)
  }
  
  onMounted(() => {
    // 마지막으로 본 letter 위치로 스크롤
    const lastLetter = localStorage.getItem('lastLetter')
    if (lastLetter) {
      setTimeout(() => {
        const sections = alphabetListRef.value.querySelectorAll('.letter-section')
        sections.forEach((section) => {
          if (section.querySelector('h2').textContent === lastLetter) {
            section.scrollIntoView({ behavior: 'smooth' })
          }
        })
      }, 100)
    }
  })
  </script>
  
  <style scoped>
  .container {
    max-width: 100%;
    margin: 0 auto;
    padding: 10px;
    height: 100vh;
  }
  
  .alphabet-list {
    height: 100vh;
    overflow-y: auto;
    scroll-snap-type: y mandatory;
  }
  
  .letter-section {
    height: 100vh;
    display: flex;
    flex-direction: column;
    padding: 20px 10px;
    scroll-snap-align: start;
  }
  
  .word-swiper {
    width: 100%;
    flex: 1;
    min-height: 0;
    position: relative;
  }
  
  .word-card {
    height: 100%;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 12px;
    background-color: #f9f9f9;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  
  .spelling {
    margin: 20px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
  }
  
  .spelling span {
    margin-right: 0;
    color: #666;
    font-size: 1.4rem;
    padding: 5px 10px;
    background-color: #fff;
    border-radius: 6px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    min-width: 120px;
    text-align: center;
  }
  
  .pronunciation {
    color: #2c3e50;
    font-weight: bold;
    font-size: 1.6rem;
    text-align: center;
  }
  
  h2 {
    color: #333;
    margin-bottom: 20px;
    font-size: 2.5rem;
    text-align: center;
  }
  
  h3 {
    color: #2c3e50;
    margin: 0 0 15px 0;
    font-size: 2rem;
    text-align: center;
  }
  
  /* Swiper 네비게이션 버튼 스타일 커스터마이징 */
  :deep(.swiper-button-next),
  :deep(.swiper-button-prev) {
    color: #2c3e50;
    background-color: rgba(255, 255, 255, 0.9);
    padding: 30px;
    border-radius: 50%;
    width: 25px;
    height: 25px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
  }
  
  :deep(.swiper-button-next:after),
  :deep(.swiper-button-prev:after) {
    font-size: 26px;
    font-weight: bold;
  }
  
  :deep(.swiper-button-next:hover),
  :deep(.swiper-button-prev:hover) {
    background-color: rgba(255, 255, 255, 1);
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
    transform: scale(1.1);
  }
  
  :deep(.swiper-button-disabled) {
    opacity: 0.35;
    cursor: not-allowed;
  }
  
  @media (max-width: 480px) {
    .container {
      padding: 5px;
    }
  
    .letter-section {
      padding: 15px 5px;
    }
  
    .word-card {
      padding: 15px;
    }
  
    h2 {
      font-size: 2.2rem;
    }
  
    h3 {
      font-size: 1.8rem;
    }
  
    .spelling span {
      font-size: 1.2rem;
      min-width: 100px;
      padding: 4px 8px;
    }
  
    .pronunciation {
      font-size: 1.4rem;
    }
  
    :deep(.swiper-button-next),
    :deep(.swiper-button-prev) {
      padding: 20px;
      width: 20px;
      height: 20px;
    }
  
    :deep(.swiper-button-next:after),
    :deep(.swiper-button-prev:after) {
      font-size: 22px;
    }
  }
  </style>