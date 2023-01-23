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
  color: #6c7fe1;
  padding: 0.25rem 0.75rem;
  font-size: 5 rem;
  font-weight: 700;
}

button:hover {
  cursor: pointer;
  background-color: #3f50b5;
  color: white;
}
</style>
