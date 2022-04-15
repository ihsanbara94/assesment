<template>
  <button class="styleButton" @click="$emit('click')">{{ content }}</button>
</template>

<script>
export default {
  props: {
    content: {
      type: String,
      default: "",
    },
  },
};
</script>

<style>
.styleButton {
  color: #52af9d;
  padding: 0.25rem 0.75rem;
  font-size: 5 rem;
  font-weight: 700;
}

button:hover {
  cursor: pointer;
  background-color: #0054d2;
}
</style>
