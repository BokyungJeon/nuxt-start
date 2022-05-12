<template>
  <div class="app">
    <main>
      <!-- :search-keyword="searchKeyword"
        @input="updateSearchKeyword" -->
      <SearchInput v-model="searchKeyword" @search="searchProducts" />
      <ul>
        <li
          class="item flex"
          v-for="product in products"
          :key="product.id"
          @click="moveToDetailPage(product.id)"
        >
          <img
            class="product-image"
            :src="product.imageUrl"
            :alt="product.name"
          />
          <p>{{ product.name }}</p>
          <span>{{ product.price }}</span>
        </li>
      </ul>
      <div class="cart-wrapper">
        <button class="btn" @click="moveToCartPage">장바구니 바로가기</button>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'
import SearchInput from '~/components/SearchInput.vue' // ~: 웹팩 resolve 옵션. Nuxt는 설정되어있어 @, ~ 상관없다.
import { fetchProductsByKeyword } from '~/api'
// import ProductList from '~/components/ProductList.vue'

export default {
  components: { SearchInput },
  // components: { ProductList },

  async asyncData() {
    // pages 아래 컴포넌트에만 제공됨. 페이지 진입 전에 호출됨.
    const response = await axios.get('http://localhost:3000/products')
    const products = response.data.map((item) => ({
      ...item,
      imageUrl: `${item.imageUrl}?random=${Math.random()}`,
    })) // api가 동일이미지 나와서 임시방편으로 랜덤이미지 생성
    return { products } // {products: products} 축약 문법
  },

  methods: {
    moveToDetailPage(id) {
      this.$router.push(`detail/${id}`) // nuxt가 기본적으로 뷰라우터를 가지고있음
    },

    // updateSearchKeyword(keyword) {
    //   this.searchKeyword = keyword
    // },
    async searchProducts() {
      const response = await fetchProductsByKeyword(this.searchKeyword)
      console.log(response.data)
      // products는 asycData에서 정의되었기 때문에 인스턴스의 데이터로 정의되어있는 상태이다.
      this.products = response.data.map((item) => ({
        ...item,
        imageUrl: `${item.imageUrl}?random=${Math.random()}`,
      })) // api가 동일이미지 나와서 임시방편으로 랜덤이미지 생성
    },
    moveToCartPage() {
      this.$router.push('/cart')
    },
  },

  data() {
    return {
      searchKeyword: '',
    }
  },

  // async created() {
  //   const response = await axios.get('http://localhost:3000/products')
  //   console.log(response)
  //   this.products = response.data
  // },
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}
.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}
.product-image {
  width: 400px;
  height: 250px;
}
.app {
  position: relative;
}
.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}
.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>
