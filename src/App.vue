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
  }
  
  .alphabet-list {
    height: 100vh;
    overflow-y: auto;
  }
  
  .letter-section {
    margin-bottom: 20px;
  }
  
  .word-swiper {
    width: 100%;
    height: 150px;
  }
  
  .word-card {
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
  }
  
  .spelling {
    margin: 10px 0;
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
  }
  
  .spelling span {
    margin-right: 5px;
    color: #666;
    font-size: 0.9rem;
  }
  
  .pronunciation {
    color: #2c3e50;
    font-weight: bold;
    font-size: 0.95rem;
  }
  
  h2 {
    color: #333;
    margin-bottom: 15px;
    font-size: 1.5rem;
  }
  
  h3 {
    color: #2c3e50;
    margin: 0 0 10px 0;
    font-size: 1.2rem;
  }
  
  @media (max-width: 480px) {
    .container {
      padding: 8px;
    }
  
    .word-card {
      padding: 12px;
    }
  
    h2 {
      font-size: 1.3rem;
    }
  
    h3 {
      font-size: 1.1rem;
    }
  
    .spelling span {
      font-size: 0.85rem;
    }
  
    .pronunciation {
      font-size: 0.9rem;
    }
  }
  </style>