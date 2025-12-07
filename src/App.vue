<script setup lang="ts">
import { ref, computed } from "vue";
import type { User } from "./types";
import UserSearch from "./components/UserSearch.vue";
import UserList from "./components/UserList.vue";
const users = ref<User[]> ([
  { id: 1, name: '山田 太郎', department: '営業部', email: 'taro@example.com' },
  { id: 2, name: '鈴木 花子', department: '人事部', email: 'hanako@example.com' },
  { id: 3, name: '佐藤 次郎', department: '開発部', email: 'jiro@example.com' },
  { id: 4, name: '田中 美咲', department: '営業部', email: 'misaki@example.com' },
  { id: 5, name: '高橋 健一', department: '開発部', email: 'kenichi@example.com' }
])
const searchText = ref('')
const handleDelete = (id: number) => {
  users.value = users.value.filter(user => user.id != id)
}
const filteredUsers = computed(() => {
  if (!searchText.value) return users.value
  const lowerText = searchText.value.toLowerCase()
  return users.value.filter(user =>
    user.name.toLocaleLowerCase().includes(lowerText)
  )
})
</script>

<template>
  <div class = "container">
    <h1 class = "title">社員名簿</h1>
    <UserSearch v-model = "searchText"/>
    <div class = "content">
      <UserList :users = "filteredUsers" @delete = "handleDelete"/>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 40px auto;
  padding: 0 20px;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  color: #333;
}

.title {
  text-align: center;
  margin-bottom: 30px;
  font-size: 24px;
  color: #2c3e50;
}
</style>
