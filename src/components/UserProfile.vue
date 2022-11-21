<script setup lang="ts">
import { defineProps } from 'vue';

interface Props {
  username: string
  nationality: string
  likes: string[]
}

const props = defineProps<Props>()
</script>

<template>
  <p class="username">{{ props.username }}</p>
  <p class="nationality" :class="props.nationality !== 'American' ? 'foreign' : 'american'">
    {{ props.nationality }}
  </p>
  <ul class="likes">
    <li class="like" v-for="like in props.likes" :key="like">
      {{ like }}
    </li>
  </ul>
</template>

<style>
.username {
  font-size: 1.5em;
  font-weight: bold;
}

.nationality {
  color: #333;
}

.foreign::after {
  content: " - Foreign!";
}

.american::after {
  content: " - Fellow American!";
}

.likes {
  display: flex;
  list-style-type: none;
  gap: 1em;
  padding-inline: 0;
}

.like {
  padding: 0.5em;
  background-color: #25aa63;
  border-radius: 0.25em;
  transition: transform 0.25s ease-in-out;
}

.like:hover {
  transform: scale(1.125);
  cursor: help;
}
</style>