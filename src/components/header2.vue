<script setup>
import { RouterView, RouterLink } from 'vue-router'
</script>

<!-- ЦЕ ШАПКА БУДЕТ -->
<template>
  <div class="category-bar">
    <RouterLink class="cat-link cat" :to="{ name: 'products', query: { kategor: 'Кошки' } }">
      <img class="category-img" style="width: 80px;" src="../img/kot.svg" alt="Логотип" />
    </RouterLink>
    <RouterLink class="cat-link dog" :to="{ name: 'products', query: { kategor: 'Собаки' } }">
      <img class="category-img" style="width: 35px; height: 80px;" src="../img/sob.svg" alt="Логотип" />
    </RouterLink>
    <RouterLink class="cat-link mouse" :to="{ name: 'products', query: { kategor: 'Грызуны' } }">
      <img class="category-img" style="width: 70px;" src="../img/mi.svg" alt="Логотип" />
    </RouterLink>
    <RouterLink class="cat-link bird" :to="{ name: 'products', query: { kategor: 'Птицы' } }">
      <img class="category-img" style="width: 60px;" src="../img/bir.svg" alt="Логотип" />
    </RouterLink>
  </div>
</template>

<style scoped>

.category-bar {
  align-items: center;
    height: 100px;
    margin-top: 0px;
    background-image: url('../img/der6.jpg'); 
  background-size: cover; 
  background-position: center; 
 
  display: flex;
  justify-content: center;
  gap: 2rem;
  padding: 0.7rem 0;
  font-family: H;
  box-shadow: 0 2px 8px rgba(27, 10, 0, 0.781); 
  height: 80px;
  
}
.category-img {
  transition: 0.3s ease-in-out;
}


.cat-link.cat img:hover {
  content: url('../img/kotg.svg');
}
.cat-link.dog img:hover {
  content: url('../img/dog.svg');
}
.cat-link.mouse img:hover {
  content: url('../img/mouse.svg');
}
.cat-link.bird img:hover {
  content: url('../img/bird.svg');
}


.cat-link {
  color: white;
  text-decoration: none;
  font-size: 18px;
  font-weight: bold;
  transition: color 0.3s;
}

.cat-link:hover {
  color: #EDF5E1;
}

@font-face {
    font-family: H;
    src: url(../styles/tu.otf);
}



</style>