<script setup>
import axios from "axios";
import UserList from "@/components/userList.vue";
import { ref, reactive, onMounted } from "vue";

const users = reactive([]);
const page = ref(1);
const limit = ref(6);
const totalPages = ref(0);

const fetchUsers = async () => {
  try {
    const response = await axios.get('https://reqres.in/api/users', {
      params: {
        page: page.value,
        per_page: limit.value
      }
    });
    users.splice(0, users.length, ...response.data.data);
    totalPages.value = Math.ceil(response.data.total / limit.value);
  } catch (e) {
    console.log(e);
  }
};

const changePage = (pageNumber) => {
  page.value = pageNumber;
  fetchUsers();
};

onMounted(fetchUsers);
</script>

<template>
  <div class="app">
    <UserList :users="users"/>
  </div>

  <div class="page__wrapper">
    <div class="page"
         v-for="pageNumber in totalPages"
         :key="pageNumber"
         :class="{'current__page': page === pageNumber}"
         @click="changePage(pageNumber)"> {{ pageNumber }}
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.page__wrapper {
  display: flex;
  justify-content: center;
  margin-top: 15px;
}

.page {
  cursor: pointer;
  padding: 5px;
}

.app {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  flex-direction: row;
}

.current__page {
  text-decoration: underline;
}
</style>