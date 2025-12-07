<script setup lang = "ts">
import type { User } from '@/types';
defineProps<{
  users: User[]
}>()
const emit = defineEmits<{
  (e: 'delete', id: number): void
}>()
</script>

<template>
  <TransitionGroup name = "list" tag = "ul" class = "grid-container">
    <li v-for="user in users" :key = "user.id" class = "user-card">
      <div class = "card-header">
        <div class = "avatar">{{ user.name.charAt(0) }}</div>
        <div class = "info">
          <span class = "name">{{ user.name }}</span>
          <span class = "dept">{{ user.department }}</span>
        </div>
      </div>

      <div class = "card-body">
        <p class = "email">{{ user.email }}</p>
      </div>

      <button @click = "emit('delete', user.id)" class = "delete-btn">
        削除
      </button>
    </li>
  </TransitionGroup>

  <div v-if = "users.length === 0" class = "empty-state">
    該当する社員は見つかりませんでした
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  list-style: none;
  padding: 0;
}

.user-card {
  background: white;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  display: flex;
  flex-direction: column;
  transition: transform 0.2s;
  border: 1px solid #f0f0f0;
}

.user-card:hover {
  transform: translateY(-5px); /* ホバーで少し浮く */
  box-shadow: 0 10px 15px rgba(0,0,0,0.1);
}

.card-header {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.avatar {
  width: 50px;
  height: 50px;
  background-color: #e0f2f1;
  color: #009688;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 20px;
  margin-right: 15px;
}

.info { display: flex; flex-direction: column; }
.name { font-weight: bold; font-size: 18px; }
.dept { font-size: 12px; color: #888; }
.email { font-size: 14px; color: #666; margin-bottom: 20px; word-break: break-all; }

.delete-btn {
  margin-top: auto; /* ボタンを一番下に押しやる */
  background-color: transparent;
  border: 1px solid #ff4d4d;
  color: #ff4d4d;
  padding: 8px;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s;
}
.delete-btn:hover {
  background-color: #ff4d4d;
  color: white;
}

.empty-state {
  text-align: center;
  color: #888;
  margin-top: 50px;
}

/* アニメーションの設定 */
.list-enter-active,
.list-leave-active {
  transition: all 0.4s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: scale(0.9);
}
</style>