<script setup lang = "ts">
defineProps<{
  modelValue: string
}>()
const emit = defineEmits<{
  (e: 'update:modelValue', value: string): void
}>()
const onInput = (e: Event) => {
  const text = (e.target as HTMLInputElement).value
  emit('update:modelValue', text)
}
</script>

<template>
  <div class = "search-box">
    <span class = "icon">🔍</span>
    <input type="text" :value = "modelValue" @input = "onInput" placeholder = "名前で検索" class = "search-input"/>
  </div>
</template>

<style scoped>
.search-box {
  position: relative;
  max-width: 400px;
  margin: 0 auto 40px; /* 中央寄せ */
}

.icon {
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  color: #aaa;
}

.search-input {
  width: 100%;
  padding: 12px 12px 12px 45px; /* アイコンの分だけ左を空ける */
  border: 1px solid #ddd;
  border-radius: 25px; /* 丸みをつける */
  font-size: 16px;
  outline: none;
  transition: all 0.3s;
  box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.search-input:focus {
  border-color: #42b883;
  box-shadow: 0 4px 10px rgba(66, 184, 131, 0.2);
}
</style>