<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import Modal from './modal.vue'

const isAuthenticated = ref(false) // ВОШЕЛ ИЛЬ НЕТ
const showAuth = ref(false) // ДЛЯ МОДАЛКИ АВТОРИЗАЦИИ
const menuOpen = ref(false)
const router = useRouter()

// СДЕЛАТЬ ТАК ЧТОБЫ ПОЛЬЗОВАТЕЛЬ АВТОМАТИЧЕСКИ АВТОРИЗОВАЛСЯ НЕ ЗАБЫТЬ 
onMounted(() => {
  const storedUser = JSON.parse(localStorage.getItem('user'))
  if (storedUser?.isAuthenticated) {
    isAuthenticated.value = true
  }
  // ЭТО ДЛЯ КОРЗИНЫ ЕСЛИ ТАМ НАЖМУТ ФОРМИТЬ ЗАКАЗ ВЫЛЕЗЕТ ЧУДОВИЩЕ
  window.addEventListener('open-auth', () => {
    showAuth.value = true
  })
})

// СДЕЛИТ ЗА УЗЕРОМ ЧТОБ ЕСЛИ ЧЕ СЮДА ЕГО КИНУТЬ
window.addEventListener('storage', () => {
  const updatedUser = JSON.parse(localStorage.getItem('user'))
  isAuthenticated.value = !!updatedUser?.isAuthenticated

  
  if (!updatedUser?.isAuthenticated && router.currentRoute.value.path === '/cabinet') 
  {
    router.push('/')
  }
})

// МОДАЛКА ВЫТЛЕТАЕТ
function handleSuccess() {
  isAuthenticated.value = true
  showAuth.value = false
  router.push('/cabinet') 
}

// ВЫХОД
function logout() {
  localStorage.removeItem('user') 
  isAuthenticated.value = false 
  router.push('/') 
}


function toggleMenu() {
  menuOpen.value = !menuOpen.value
}
</script>

<template>
  <nav class="navbar">
    
    <div class="sss">
      <RouterLink to="{ name: 'home' }">
        <img class="log default" src="../img/baddy.png" alt="Логотип" />
      </RouterLink>
    </div>

   
    <button class="burger" @click="toggleMenu">☰</button>

    
    <ul class="links center-links" :class="{ open: menuOpen }">
      <li class="underline-one"><RouterLink to="{ name: 'home' }">Главная</RouterLink></li>
      <li class="underline-one"><RouterLink to="{ name: 'about' }">О нас</RouterLink></li>
      <li class="underline-one"><RouterLink to="{ name: 'products' }">Товары</RouterLink></li>
      <li class="underline-one"><RouterLink to="{ name: 'gallery' }">Контакты</RouterLink></li>
      <RouterLink :to="{ name: 'home', hash: '#ask-section' }">FAQ</RouterLink>
    </ul>

    
    <ul class="links right-links" :class="{ open: menuOpen }">
  
  <li>
    <RouterLink to="{ name: 'karzine' }">
      <img class="log-lav lav" src="../img/kar23.png" alt="Корзина" />
    </RouterLink>
  </li>
  <li>
    <RouterLink to="{ name: 'love' }">
      <img class="log-kar kar " src="../img/like.png" alt="Корзина" />
    </RouterLink>
  </li>
  <li @click="isAuthenticated ? router.push({ name: 'cabinet' }) : showAuth = true" style="cursor: pointer;">
    <img class="log-kab kab" src="../img/ak23.png" alt="Кабинет" />
  </li>
</ul>
  </nav>

  
  <Modal v-if="showAuth" @close="showAuth = false" @success="handleSuccess" />
</template>



<style scoped>
.underline-one {
	color: #00bfff; 
    position: relative;
    cursor: pointer;
    text-decoration: none; 
}
.underline-one:after {
	content: "";
    display: block;
    position: absolute;
    right: 0;
    bottom: -3px;
    width: 0;
    height: 2px; 
    background-color: black; 
    transition: width 0.5s;
}

.underline-one:hover:after {
	content: "";
    width: 100%;
    display: block;
    position: absolute;
    left: 0;
    bottom: -3px;
    height: 2px; 
    background-color: rgb(53, 168, 31); 
    transition: width 0.5s;  
}
     
.category-bar {
  background-color: #05386B; 
  display: flex;
  justify-content: center;
  gap: 2rem;
  padding: 0.7rem 0;
  font-family: H;
  box-shadow: 0 2px 8px rgba(0, 31, 39, 0.7);
  
}
.category-img {
  transition: 0.3s ease-in-out;
}





.cat-link {
  color: white;
  text-decoration: none;
  font-size: 18px;
  font-weight: bold;
  transition: color 0.3s;
}
.log-lav{
  width: 40px;
  transition: color 0.3s;
}
.log-kar{
  width: 40px;
  transition: color 0.3s;
}

.log-ext{
  width: 40px;
  transition: color 0.3s;
}
.log-lav:hover {
  content: url('../img/i.png');
}

.log-kar:hover {
  content: url('../img/m.png');
}

.log-kab:hover {
  content: url('../img/k.png');
}


.log-kab{
  width: 40px;
}


.sss{
  
  display: flex;
  align-items: center;
  margin-left: 159px;
}
.log{
  
  width: 150px;
  transition: opacity 0.3s ease-in-out;
}
.log:hover{
  width: 151px;
}

.schapka{
  flex: 1;
  display: flex;
  justify-content: center; 

}
@font-face {
    font-family: H;
    src: url(../styles/tu.otf);
}
.navbar{
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #2c5140;
  padding: 0 2rem;
  height: 100px;
  font-family: H;
  background-size: cover;
  font-size: 15px;
  

}

.links{
    display: flex;
    gap: 1.5rem;
    list-style:none
    
}
.center-links {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
.right-links {
 
  color: #cccccc;
  display: flex;
  gap: 1.5rem;
  margin-right: 70px;
   transition: 0.3s ease-in-out;
}

/* АДАПТАЦИЯ */
@media (max-width: 1024px) {
  .navbar {
    flex-wrap: wrap;
    height: auto;
    padding: 1rem;
  }

  .center-links {
    position: static;
    transform: none;
    justify-content: center;
    flex-wrap: wrap;
    width: 100%;
    margin: 1rem 0;
  }

  .links {
    justify-content: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .right-links {
    justify-content: center;
    margin: 0 auto;
  }

  .sss {
    justify-content: center;
    margin: 0 auto;
  }

  .log {
    width: 120px;
  }

  .log:hover {
    width: 140px;
  }
}

@media (max-width: 600px) {
  .navbar {
    flex-direction: column;
    align-items: center;
    
  }

  .log {
    width: 100px;
  }

  .log:hover {
    width: 120px;
  }

  .links {
    flex-direction: column;
    align-items: center;
  }

  .right-links {
    flex-direction: row;
    justify-content: center;
    gap: 1rem;
  }

  .underline-one {
    font-size: 14px;
  }
}
.burger {
  display: none;
  font-size: 2rem;
  background: none;
  border: none;
  cursor: pointer;
  color: white;
  z-index: 1000;
  
  
}

@media (max-width: 768px) {
  .burger {
    display: block;
    position: absolute;
    right: 1rem;
    
  }

  .center-links,
  .right-links {
    display: none;
    flex-direction: column;
    width: 100%;
    background-color: #2c5140;
    padding: 1rem 0;
    text-align: center;
  }

  .center-links.open,
  .right-links.open {
    display: flex;
  }

  .navbar {
    flex-wrap: wrap;
    justify-content: space-between;
  }
}

</style>