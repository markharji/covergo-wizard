<template>
  <div class="w-1/4 short-summary shadow-lg">
    <template v-if="showSummary">
      <h2>
        Your Premium is: <span>{{ premiumRate }}</span>
      </h2>

      <div class="actions">
        <button
          class="bg-red-900 hover:bg-red-700 text-white font-bold py-2 px-8 rounded"
          @click="navigate('home')"
        >
          Back
        </button>
        <button
          class="bg-green-900 hover:bg-green-700 text-white font-bold py-2 px-8 rounded"
          :disabled="!formIsValid"
          :class="{
            'bg-green-300 hover:bg-green-300 cursor-not-allowed': !formIsValid,
          }"
          @click="navigate('next')"
        >
          Next
        </button>
      </div>
    </template>
    <template v-else>
      <p class="text-center flex justify-center items-center mb-2">
        Please Fillup the following Fields
      </p>
      <button
        class="bg-red-900 hover:bg-red-700 text-white font-bold py-2 px-8 rounded"
        @click="navigate('home')"
      >
        Go Back!
      </button>
    </template>
  </div>
</template>

<script>
export default {
  name: "ShortSummary",
  data() {
    return {
      showSummary: false,
      formIsValid: false,
    };
  },
  props: {
    premiumRate: {
      type: String,
      default: "",
    },
    userDetails: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
    navigate(whereTo) {
      switch (whereTo) {
        case "home":
          //   this.$router.push({ name: "home" });
          this.$emit("goBack");
          break;
        case "next":
          this.$emit("goNext");
          break;
      }
    },
  },
  watch: {
    userDetails: {
      deep: true,
      immediate: true,
      handler(val) {
        this.showSummary = val.age && val.country;
        this.formIsValid = val.age && val.country && val.name;
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.short-summary {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #0b4141bb;
  color: #faf0dc;
}

.actions {
  button {
    margin: 5px;
  }
}
</style>
