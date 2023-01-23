<template>
  <div class="container shadow">
    <NuxtLink to="/">
      <img
        :src="require('~/assets/images/seakunid.png')"
        width="40"
        height="40"
        alt="image not found"
        class="rounded-full"
    /></NuxtLink>

    <span style="font-weight: 700; color: #52af9d">Seakun.id</span>
  </div>
</template>

<script>
export default {};
</script>

<style>
* {
  margin: 0;
}
.container {
  display: flex;
  align-items: center;
  background-color: white;
  width: 100%;
  padding: 0.5rem;
}

.rounded-full {
  border-radius: 9999px;
  margin-right: 8px;
}

.shadow {
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
}
</style>
