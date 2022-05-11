<template>
  <div>
    <div class="container">
      <div class="main-panel">
        <img
          :src="product.imageUrl"
          :alt="product.name"
          class="product-image"
        />
      </div>
      <div class="side-panel">
        <p class="name">{{ product.name }}</p>
        <p class="price">{{ product.price }}</p>
        <!-- <button type="button" @click="addToCart">Add to Cart</button> -->
      </div>
    </div>
  </div>
</template>

<script>
import { fetchProductById } from '@/api/index'

export default {
  async asyncData({ params }) {
    // context를 distructuring해서 params
    // context 속성은 넉스트 프레임워크 전반에 걸쳐 공용으로 사용됨(플러그인, 미들웨어에서도 접근가능)
    // 스토어, 라우터, 서버사이드에서 요청, 응답 관련된 속성도 접근할 수 있다.
    const response = await fetchProductById(params.id)
    const product = response.data
    return { product }
  },
  //   created() {
  //     const id = console.log(this.$route.params.id)
  //   },
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  margin: 2rem 0;
}
.product-image {
  width: 500px;
  height: 375px;
}
.side-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 220px;
  text-align: center;
  padding: 0 1rem;
}
</style>
