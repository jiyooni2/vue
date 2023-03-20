<script lang="ts">
export default {
  props: {
    firstName: {
      type: String,
      default: "",
    },

    lastName: {
      type: String,
      default: "",
    },
  },

  emits: ["update:firstName", "update:lastName"],

  beforeUpdate() {
    //check binding
    console.log(this.firstName);
    console.log(this.lastName);
  },
};
</script>

<template>
  <input
    :value="firstName"
    @input="
      $emit('update:firstName', ($event.target as HTMLInputElement).value)
    "
  />

  <input
    :value="lastName"
    @input="$emit('update:lastName', ($event.target as HTMLInputElement).value)"
  />
</template>
