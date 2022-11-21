<script setup lang="ts">
import { ref, watch, type Ref } from 'vue';
import UserProfile from './components/UserProfile.vue';

interface User {
  username: string
  nationality: string
  likes: string[]
}

const userBase: User[] = [
  {
    username: 'Ticiano Morvan',
    nationality: 'Spanish',
    likes: ['Programming', 'Voleyball', 'Videogames']
  },
  {
    username: 'Josh',
    nationality: 'American',
    likes: ['Videogames', 'Pool', 'Jokes']
  }
]

const query = ref("")

const queryUsers: Ref<User[]> = ref(userBase.filter((user) => user.username.includes(query.value)))

watch(query, (value) => {
  queryUsers.value = userBase.filter((user) => user.username.toLowerCase().includes(value.toLowerCase()))
})

</script>

<template>
  <main>
    <span class="search-bar">
      <label for="search-bar">Search user</label>
      <input id="search-bar" v-model="query" />
    </span>

    <UserProfile
      v-for="user in queryUsers"
      :key="user.username"
      :username="user.username"
      :nationality="user.nationality"
      :likes="user.likes"
    />
  </main>
</template>

<style scoped>
  .search-bar {
    display: flex;
    gap: 0.5em;
    align-items: center;
  }

  .search-bar input {
    border-radius: 0.25em;
    outline: none;
    border: 1px solid #247242aa;
    padding: 0.25em;
  }

  .search-bar input:focus-visible {
    box-shadow: 0 0 0.25em #24724a99;
  }
</style>
