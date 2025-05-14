<template>
    <div class="carousel">
      <div
        class="slide"
        v-for="(slide, index) in slides"
        :key="index"
        :class="{ active: index === currentSlide }"
        :style="{ backgroundImage: `url(${slide})` }"
      ></div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted } from 'vue'
  
  const slides = [
  new URL('../img/reck2.svg', import.meta.url).href,
  new URL('../img/rec6.svg', import.meta.url).href,
  new URL('../img/rec5.svg', import.meta.url).href,
  ]
  
  const currentSlide = ref(0)
  let interval = null
  
  onMounted(() => {
    interval = setInterval(() => {
      currentSlide.value = (currentSlide.value + 1) % slides.length
    }, 5000) 
  })
  
  onUnmounted(() => {
    clearInterval(interval)
  })
  </script>
  
  <style scoped>
.carousel {
  position: relative;
  top: 0px;
  left: 0;
  width: 100%;
  height: 500px; 
  overflow: hidden;
  margin: 0 auto;
}

.slide {
  position: absolute;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  opacity: 0;
  transition: opacity 1s ease-in-out;
}

.slide.active {
  opacity: 1;
  z-index: 1;
}


@media (max-width: 768px) {
  .carousel {
    display: none; 
  }
}


.carousel-bg {
  background: white;
  padding: 2rem;
  margin-top: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 100%; 
}

.reco-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-left: 20px;
  margin-top: 20px;
  flex-direction: column; 
}

.reco-header h2 {
  font-family: H;
  font-size: 24px; 
  color: darkgreen;
  margin: 0;
}

.cat-img {
  width: 40px; 
  height: auto;
}


.article-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 1rem;
}

@font-face {
  font-family: H;
  src: url(../styles/tu.otf);
}

h2 {
  font-family: H;
  margin-left: 50px;
  margin-top: 50px;
}

.articles-section {
  padding: 2rem;
}


@media (max-width: 480px) {
  h2 {
    font-size: 24px; 
    margin-left: 20px;
  }

  .carousel-section {
    padding: 1rem; 
  }

  .cat-img {
    width: 30px;
  }

  .article-grid {
    grid-template-columns: 1fr; 
  }
}
</style>

