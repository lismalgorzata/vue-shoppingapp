<template>
  <div class="filterWrapper">
    <div class="topFlex">
      <button
        @click="setActiveCategory('')" 
        :class="{ 'activeCategory': activeCategory === '' }"
        class="category">
        All Products
      </button>
      <div 
      :class = "activeCategory === item ? 'activeCategory' : ''"
        @click="activeCategory = activeCategory === item ? '' : item" 
        v-for="item in categories" 
        class="category">
          {{ item }}
      </div>
    </div>
    <div class="box">
      <div class="badge"> {{ choseProduct.length }}</div>
      <svg 
      @click="onShow"
        width="24" 
        height="24" 
        viewBox="0 0 24 24" 
        fill="none" 
        stroke="currentColor" 
        stroke-width="2" 
        stroke-linecap="round" 
        stroke-linejoin="round" 
        class="feather feather-shopping-cart">
          <circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/>
          <path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/>
      </svg>  
      <ShopContext @on-go-basket="show = false" v-if="show" :item="choseProduct"/>
    </div>
  </div>
  <div class="bottomFlex">
    <ProductCard @on-item-box="onItemFunc($event)" v-for = "item in products" :item = "item" />
  </div>
</template>

<script setup>
import ProductCard from '@/components/ProductCard.vue';
import ShopContext from '@/components/ShopContext.vue';
import { ref, onMounted, watch } from "vue";
const show = ref(false);
const categories = ref([]);
const products = ref([])
const choseProduct = ref([])
const activeCategory = ref(null);
const onShow = () => {
  show.value = !show.value;
};

const onItemFunc = (e) => {
  choseProduct.value.push(e);
};

const setActiveCategory = (category) => {
  activeCategory.value = category;
  if (category === '') {
    fetchProducts();
  } else {
    fetchProductByCategory(category);
  }
};

const fetchCategories = async () => {
  try {
    const response = await fetch('https://fakestoreapi.com/products/categories');
    const jsonData = await response.json();
    categories.value = jsonData;
    console.log(categories.value)
  } catch (error) {
    console.log(error);
  }
};

const fetchProducts = async () => {
  try {
    const response = await fetch('https://fakestoreapi.com/products');
    const jsonData = await response.json();
    products.value = jsonData;
    console.log(products.value)
  } catch (error) {
    console.log(error);
  }
};

const fetchProductByCategory = async (product) => {
  try {
    const response = await fetch('https://fakestoreapi.com/products/category/' + product);
    const jsonData = await response.json();
    products.value = jsonData;
  } catch (error) {
    console.log(error);
  }
};

watch(activeCategory, (newVal) => {
  if ( newVal === "" ){
    fetchProducts();
  } else {
    fetchProductByCategory(newVal);
  }
  
});

onMounted(() => {
  fetchProducts();
});

onMounted(() => {
  fetchCategories();
});

</script>

<style scoped>
.filterWrapper{
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  flex-wrap: wrap;
}

.topFlex{
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}
.category{
  cursor: pointer;
  padding: 4px 16px;
  background-color: #fafafa;
  border: 1px solid grey;
  font-size: 13px;
  font-weight: 500;
  font-family: 'Rajdhani', sans-serif;
  border-radius: 16px;
  margin-top: 8px;
}
.category:hover{
  background-color: rgb(190, 161, 190);
}
.activeCategory{
  border: 1px solid rgb(89, 28, 147);
  background: blueviolet;
  color: white;
  font-weight: 600;
}
.box{
  position: relative;
  cursor: pointer;
  color: rgb(125, 42, 153);
  transition: all 0.5s;
}

.box:hover{
  color: rgb(125, 42, 153);
}
.badge{
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -8px;
  right: -8px;
  font-size: 10px;
  background-color: rgb(125, 42, 153);
  border-radius: 100%;
  color: white;
  width: 16px;
  height: 16px;
}
.bottomFlex{
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  flex-wrap: wrap;
  margin-top: 16px;
}
</style>
