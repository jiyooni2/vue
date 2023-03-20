<script lang="ts">
export default {
  // props: ["title"],
  props: {
    title: String,
  },
  data() {
    return {
      count: 1,
    };
  },
  methods: {
    increment() {
      this.count++;
    },
  },
};
</script>

<template>
  <h1>{{ title }}</h1>
  <h2>{{ count }}번 클릭했습니다.</h2>
  <button @click="increment">count++</button>
</template>
