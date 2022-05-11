<template>
  <div>
    {{ products }}
  </div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData() {
    // pages 아래 컴포넌트에만 제공됨. 페이지 진입 전에 호출됨.
    const response = await axios.get('http://localhost:3000/products')
    console.log(response)
    const products = response.data
    return { products } // {products: products} 축약 문법
  },
}
</script>

<style></style>
