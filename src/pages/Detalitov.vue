<script setup>
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { kart } from '../composables/useProduct'
import { computed } from 'vue'
import { useCart } from '../composables/useCart' 
const router = useRouter()
const route = useRoute()
const product = kart.find(p => p.id === Number(route.params.id))
const showMore = ref(false)
const formattedSostav = computed(() =>
  (product?.sostav || 'Нет состава').replace(/\n/g, '<br>')

)
const nazad = () => {
  router.back()
}
const { addToCart } = useCart()
</script>

<template>
    <div v-if="product" class="product-detail">
      <div class="product-main">
        
        <img :src="product.image" alt="Фото товара" class="product-image" />
        
    
        <div class="product-text">
          
          <h1 class="product-title">{{ product.nasvanie }}</h1>
    
          <div class="product-info">
            <p><strong>Категория:</strong> {{ product.kategor }}</p>
            <p><strong>Бренд:</strong> {{ product.brand }}</p>
            <p><strong>Цена:</strong> {{ product.rubli }} ₽</p>
            <p><strong>Вес:</strong> {{ product.ves || 'Нет информации' }} </p>
          </div>
          <button @click="nazad" class="underline-one">Назад</button>
    
          
    
          <transition name="fade">
  <div class="product-description">
    <h3>Описание</h3>
    <p>{{ product.podrob || 'Нет описания' }}</p>
    <p><strong>Состав:</strong></p>
    <p v-html="formattedSostav"></p>
    
    <link href="//maxcdn.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css" rel="stylesheet">
    <button @click="addToCart(product)" class="btn btn-2 btn-sep icon-cart">В корзину</button>
  </div>
</transition>

        </div>
      </div>
    </div>
  </template>

<style scoped>
.btn {
  
  border: none;
  font-family: 'Lato';
  font-size: inherit;
  color: inherit;
  background: none;
  cursor: pointer;
  /* размер основной кнопки */
  padding: 8px 12px; 
  display: inline-block;
  margin: 8px auto 0 auto;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 700;
  outline: none;
  position: relative;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;
  font-size: 13px;
  width: 150px;
}

.btn:after {
  content: '';
  position: absolute;
  z-index: -1;
  -webkit-transition: all 0.3s;
  -moz-transition: all 0.3s;
  transition: all 0.3s;
}

.btn:before {
  font-family: 'FontAwesome';
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  position: relative;
  -webkit-font-smoothing: antialiased;
}

.btn-sep {
  padding: 10px 20px 10px 50px;
}

.btn-sep:before {
  background: rgba(0,0,0,0.15);
}

.btn-2 {
  font-family: H;
  background: #2ecc71;
  color: #fff;
}

.btn-2:hover {
  background: #0a6630;
}

.btn-2:active {
  background: #27ae60;
  top: 2px;
}

.btn-2:before {
  position: absolute;
  height: 100%;
  left: 0;
  top: 0;
  line-height: 2.2;
  font-size: 120%;
  width: 30px;
}
.icon-cart:before {
  content: "\f07a";
}

.icon-heart:before {
  content: "\f55a";
}

.icon-info:before {
  content: "\f05a";
}

.icon-send:before {
  content: "\f1d8";
}
.underline-one {
  
  width: min(200px, 100%);
  width: 100px;
  font-family: H;
  font-size: 16px;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  background-image: 
    linear-gradient(rgba(0, 0, 0, 0), rgba(47, 91, 53, 0.866)), 
    url('../img/der6.jpg');
  background-size: cover;
  background-position: center;
  background-blend-mode: multiply;
  cursor: pointer;
  transition: filter 0.3s ease, transform 0.2s ease;
  box-shadow: 0 4px 6px rgba(0,0,0,0.2);
}

.underline-one:hover {
  background-image: 
    linear-gradient(rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.1)), 
    url('../img/der6.jpg');
  transform: scale(1.03);
}
.back-button {
  margin-top: 1rem;
  padding: 0.6rem 1.2rem;
  font-size: 15px;
  background: #ddd;
  color: black;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s ease;
}

.back-button:hover {
  background: #ccc;
}
.product-main {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
  align-items: flex-start;
}

.product-image {
  width: 400px;
  max-height: 400px;
  object-fit: cover;
  border-radius: 12px;
  flex-shrink: 0;
}

.product-text {
  flex: 1;
  min-width: 300px;
  max-width: 600px;
}

.product-description p {
  white-space: pre-line;
  line-height: 1.5;
  font-size: 14px;
  margin-top: 0.5rem;
}
.product-detail {
  max-width: 100%;
  margin: 2rem auto;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  padding: 2rem;
  text-align: center;
  font-family: Arial, sans-serif;
}

.product-image {
  width: 400px;
  max-height: 400px;
  object-fit: cover;
  border-radius: 12px;
  margin-bottom: 1rem;
}

.product-title {
  font-size: 28px;
  margin-bottom: 1rem;
  font-weight: bold;
  color: #333;
}

.product-info p {
  font-size: 16px;
  margin: 0.3rem 0;
}

.toggle-button {
  margin-top: 1rem;
  padding: 0.6rem 1.2rem;
  font-size: 15px;
  background: #2c5243;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s ease;
}

.toggle-button:hover {
  background: #3b6b57;
}

.product-description {
  margin-top: 1.5rem;
  text-align: left;
  background: #f9f9f9;
  padding: 1rem;
  border-radius: 12px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>