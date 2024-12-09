<script setup lang="ts">
import { ref } from "vue";
import Form from "./components/Form.vue";
import Table from "./components/Table.vue";
import Data from "./components/Data.vue";

const users = ref([
  {
    firstName: "Marcos",
    lastName: "Portales",
    email: "marcos@fadas",
    age: 22,
    sex: "F",
    nacionality: "Cuba",
  },
]);

const add_new_user = (user) => {
  users.value.push(user);
};
</script>

<template>
  <main class="flex flex-col gap-y-10 p-4">
    <Form :add_new_user="add_new_user" />
    <div class="flex flex-col lg:flex-row gap-10">
      <Table :users="users" />
      <Data :users="users" />
    </div>
  </main>
</template>
