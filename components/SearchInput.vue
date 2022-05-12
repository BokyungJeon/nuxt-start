<template>
  <div class="input-wrapper flex">
    <input
      type="text"
      :value="value"
      class="search-input"
      @input="$emit('input', $event.target.value)"
    />
    <button class="btn" type="button" @click="$emit('search')">search</button>
    <!-- 유닛테스트를 위해서는 @click을 메서드로 분류하는 것이 좋은코드 -->
  </div>
</template>

<script>
export default {
  props: {
    // searchKeyword: {
    // model: {} // value가 아닌 다른 props이름을 사용하고 싶을 때 사용.
    value: {
      // v-model사용하면 props는 value로 사용해야한다.
      type: String,
      default: () => '',
    },
  },
}
</script>

<style scoped>
.input-wrapper {
  height: 40px;
  margin: 1rem 0;
}

.search-input {
  width: 200px;
  font-size: 1.2rem;
  font-weight: 500;
}

.btn {
  font-size: 1.2rem;
  font-weight: 500;
}
</style>
