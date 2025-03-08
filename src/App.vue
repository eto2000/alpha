<template>
    <div class="container">
      <div class="alphabet-list">
        <div v-for="item in alphabetData.alphabet" :key="item.letter" class="letter-section">
          <h2>{{ item.letter }}</h2>
          <swiper
            :slides-per-view="1"
            :space-between="30"
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
  import 'swiper/css'
  import alphabetData from './assets/alphabet-data.json'
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
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }
  
  .spelling span {
    margin-right: 8px;
    color: #666;
    font-size: 1.4rem;
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
    }
  
    .pronunciation {
      font-size: 1.4rem;
    }
  }
  </style>