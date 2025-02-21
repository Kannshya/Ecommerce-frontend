<template>
  <div class="home">
    <!-- 导航栏 -->
    <nav class="navbar">
      <div class="logo">YizhuEcommerce</div>
      <div class="search-box">
        <input type="text" placeholder="搜索商品..." v-model="searchQuery" />
        <button @click="search">搜索</button>
      </div>
      <div class="user-actions">
        <router-link to="/login">登录</router-link>
        <router-link to="/register">注册</router-link>
      </div>
    </nav>

    <!-- 轮播图 -->
    <!-- <div class="carousel">
      <img :src="currentBanner" alt="Banner" />
      <div class="carousel-controls">
        <button @click="prevBanner">上一张</button>
        <button @click="nextBanner">下一张</button>
      </div>
    </div> -->

    <!-- 商品分类 -->
    <div class="categories">
      <h2>商品分类</h2>
      <div class="category-list">
        <div v-for="category in categories" :key="category.id" class="category-item">
          <el-icon >
            <component :is="category.icon" />
          </el-icon>
          <p>{{ category.name }}</p>
        </div>
      </div>
    </div>

    <!-- 热门商品 -->
    <div class="hot-products">
      <h2>热门商品</h2>
      <div class="product-list">
        <div v-for="product in hotProducts" :key="product.id" class="product-item">
          <img :src="product.image" :alt="product.name" />
          <h3>{{ product.name }}</h3>
          <p class="price">￥{{ product.price }}</p>
          <button @click="addToCart(product)">加入购物车</button>
        </div>
      </div>
    </div>

    <!-- 页脚 -->
    <footer class="footer">
      <p>&copy; 2025 YizhuEcommerce. All rights reserved.</p>
      <p>联系我们: jp2021212716@qmul.ac.uk</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

// 搜索框
const searchQuery = ref<string>("");

// 轮播图
const banners = ref<string[]>([
  "https://via.placeholder.com/1200x400?text=Banner+1",
  "https://via.placeholder.com/1200x400?text=Banner+2",
  "https://via.placeholder.com/1200x400?text=Banner+3",
]);
const currentBannerIndex = ref<number>(0);
const currentBanner = computed(() => banners.value[currentBannerIndex.value]);

import {
  ForkSpoon,
  Goods ,
  House,
  Reading,
  Phone ,
  Coordinate
} from '@element-plus/icons-vue';

// 商品分类
interface Category {
  id: number;
  name: string;
  icon: any;
}
const categories = ref<Category[]>([
  { id: 1, name: "电子产品Electronics", icon: Phone },
  { id: 2, name: "服装Clothes", icon: Goods },
  { id: 3, name: "家居Home", icon: House },
  { id: 4, name: "图书Books", icon: Reading },
  { id: 5, name: "办公用品Office Supplies", icon: Coordinate },
  { id: 6, name: "食品Food", icon: ForkSpoon }
]);

// 热门商品
interface Product {
  id: number;
  name: string;
  price: number;
  image: string;
}

const hotProducts = ref<Product[]>([
  { id: 1, name: "iPhone 14", price: 6999, image: "https://th.bing.com/th/id/OIP._na13jK8xtmI0kS6hRS7ywHaFj?rs=1&pid=ImgDetMain" },
  { id: 2, name: "MacBook Pro", price: 12999, image: "https://cdn2.vox-cdn.com/uploads/chorus_asset/file/7390261/vpavic_161031_1256_0264.0.jpg" },
  { id: 3, name: "T-shirt for women", price: 200, image: "https://img.alicdn.com/bao/uploaded/i1/1701538797/O1CN01U6Plpo2Er4mfNgrW1_!!1701538797.jpg" },
  { id: 4, name: "instant rice noodles", price: 25, image: "https://th.bing.com/th/id/OIP.7z5iu9JWo7pV99NWySyExwHaHa?rs=1&pid=ImgDetMain" },
]);

// 方法
const search = () => {
  if (searchQuery.value.trim()) {
    alert(`搜索: ${searchQuery.value}`);
  } else {
    alert("请输入搜索内容");
  }
};

const prevBanner = () => {
  currentBannerIndex.value = (currentBannerIndex.value - 1 + banners.value.length) % banners.value.length;
};

const nextBanner = () => {
  currentBannerIndex.value = (currentBannerIndex.value + 1) % banners.value.length;
};

const addToCart = (product: Product) => {
  alert(`已加入购物车: ${product.name}`);
};
</script>

<style scoped>
.home {
  font-family: Arial, sans-serif;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background-color: #333;
  color: white;
}

.logo {
  font-size: 24px;
  font-weight: bold;
}

.search-box input {
  padding: 5px;
  margin-right: 10px;
}

.search-box button {
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.user-actions a {
  margin-left: 10px;
  color: white;
  text-decoration: none;
}

.carousel {
  position: relative;
  text-align: center;
}

.carousel img {
  width: 100%;
  height: 400px;
  object-fit: cover;
}

.carousel-controls {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
}

.carousel-controls button {
  margin: 0 5px;
  padding: 5px 10px;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  cursor: pointer;
}

.categories {
  padding: 20px;
  text-align: center;
}

.category-list {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.category-item {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 160px; /* 固定宽度 */
  height: 30px; /* 固定高度 */
  border: 1px solid #ddd; 
  padding: 3px;
  box-sizing: border-box;/* 一种计算方式，使总width = width + paadding + border */
}

.category-item el-icon {
  width: 15px; /* 统一宽度 */
  height: 15px; /* 统一高度 */
  display: flex;
  margin-right: 3px; /* 让图标与文字之间有间距 */
  margin-bottom: 3px;
}

.category-item p {
  font-size: 12px;
  white-space: nowrap; /* 防止文字换行 */
}


.hot-products {
  padding: 20px;
  text-align: center;
}

.product-list {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.product-item {
  width: 200px;
  text-align: center;
}

.product-item img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.product-item h3 {
  margin: 10px 0;
}

.product-item .price {
  color: #e44d26;
  font-weight: bold;
}

.product-item button {
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.footer {
  padding: 20px;
  background-color: #333;
  color: white;
  text-align: center;
}
</style>
