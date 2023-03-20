<script lang="ts">
export default {
  // props: ["title"],

  props: {
    title: String,
    initialLikes: {
      type: Number,
      required: true,
      // default:100
    },
  },
  data() {
    return {
      view: 0,
      likes: this.initialLikes,
    };
  },
  methods: {
    like() {
      this.likes++;
    },
  },
};
</script>

<template>
  <div>
    <h1>{{ title }}</h1>
    <p>{{ view }} Seen</p>
    <p>{{ likes }} Likes</p>

    <button @click="view++">See</button>
    <button @click="like">likes++</button>
  </div>
</template>
