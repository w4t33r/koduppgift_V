<script setup>

import {defineProps} from "vue";

defineProps({
  users: {
    type: Object,
    required: true
  }
})

const fullName =  (user) => {
  return user.first_name + ' ' + user.last_name
}
</script>

<template>
  <div class="wrapper" v-for="user in users" :key="user.id">
    <div class="user-card">
      <img alt="avatar" class="avatar" :src="user.avatar"/>
      <div class="cards__items"><strong>{{fullName(user)}}</strong></div>
      <div class="cards__items"> email:
        <a class="cards__links" v-bind:href="'mailto:' + user.email">{{ user.email }}</a>
      </div>

    </div>
  </div>
</template>

<style scoped>
.user-card {
  width: 260px;
  height: 260px;
  margin: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  border-radius: 10px;
  background: #eaeaea;
}

.wrapper {
  display: flex;
  align-items: flex-start;
}

.cards__items {
  margin-top: 20px;
  display: flex;
  justify-content: center;

}
.cards__links {
  text-underline: none;
  margin-left: 5px;
  text-decoration: none;
  color:rebeccapurple;
}

.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
}
</style>