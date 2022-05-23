<template>
  <div class="page-error rounded shadow-lg w-1/4">
    <h1 class="m-4">Ooops.</h1>
    <p class="m-4">
      Your age is over our accepted limit. We are sorry but we cannot insure you
      now
    </p>

    <button class="error-button py-4 px-8 rounded m-8" @click="$emit('home')">
      Ok :(
    </button>
  </div>
</template>

<script>
export default {
  name: "PageError",
};
</script>

<style lang="scss" scoped>
.page-error {
  background: #0b4141;
  color: #faf0dc;
}

h1 {
  font-size: 2rem;
  font-weight: 800;
}

p {
  text-align: center;
}

.error-button {
  background: #ff6864;
  color: #faf0dc;
}

.error-button:hover {
  background: red;
}
</style>
