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
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .alphabet-list {
    height: 100vh;
    overflow-y: auto;
  }
  
  .letter-section {
    margin-bottom: 40px;
  }
  
  .word-swiper {
    width: 100%;
    height: 200px;
  }
  
  .word-card {
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
  }
  
  .spelling {
    margin: 15px 0;
  }
  
  .spelling span {
    margin-right: 10px;
    color: #666;
  }
  
  .pronunciation {
    color: #2c3e50;
    font-weight: bold;
  }
  
  h2 {
    color: #333;
    margin-bottom: 20px;
  }
  
  h3 {
    color: #2c3e50;
    margin: 0 0 15px 0;
  }
  </style>