<template>
  <div class="landing-page h-screen">
    <div class="jumbotron shadow-lg">
      <h1 class="text-center font-bold header-text">Hello There!</h1>
      <p class="mb-8 mt-8">
        Let's buy some insurance. It is going to take only a few steps
      </p>
      <router-link class="font-bold py-4 px-8 rounded button-start" to="/wizard"
        >Start!</router-link
      >
    </div>
  </div>
</template>

<script>
// @ is an alias to /srcss

export default {
  name: "HomeView",
};
</script>

<style scoped lang="scss">
.landing-page {
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.jumbotron {
  width: 60%;
  padding: 100px 50px 100px 50px;
  background: #0b4141;
  color: #faf0dc;
}

.header-text {
  font-size: 2.5rem;
}

.button-start {
  color: #faf0dc;
  background: #ff6864;
}

.button-start:hover {
  background: red;
}
</style>
