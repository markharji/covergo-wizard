<template>
  <div class="final-summary w-3/4 rounded shadow-xl py-20 h-fit">
    <div class="header-summary h-fit">
      <h1>Summary</h1>
      <h2>
        Hi <span class="font-bold">{{ userDetails.name }}</span
        >,
      </h2>
    </div>

    <div class="transaction-details">
      <p>
        Name : <span>{{ userDetails.name }}</span>
      </p>
      <p>
        Age : <span>{{ userDetails.age }}</span>
      </p>
      <p>
        Where Do you live : <span>{{ userDetails.country }}</span>
      </p>
      <p>
        Package:
        <span>{{
          selectedPremium === "superSafe" ? "Super Safe" : selectedPremium
        }}</span>
      </p>
      <p>
        Premium: <span>{{ premiumRate }}</span>
      </p>
    </div>

    <div class="actions">
      <button
        class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-8 rounded"
        @click="$emit('goBack')"
      >
        Back
      </button>
      <button
        class="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-8 rounded"
        @click="navigate('home')"
      >
        Buy
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "FinalSummary",
  props: {
    premiumRate: {
      type: String,
      default: "",
    },
    userDetails: {
      type: Object,
      default: () => {},
    },
    selectedPremium: {
      type: String,
      default: "Standard",
    },
  },
  methods: {
    navigate(whereTo) {
      switch (whereTo) {
        case "home":
          this.$router.push({ name: "home" });
          break;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.final-summary {
  background: #0b4141;
  color: #faf0dc;
}

.actions {
  button {
    margin: 5px;
  }
}

.header-summary {
  height: fit-content;

  h1 {
    font-size: 1.5rem;
    font-weight: 600;
  }
  h2 {
    font-size: 1rem;
  }
}

.transaction-details {
  margin-top: 24px;
  margin-bottom: 40px;
  p {
    margin: 5px;
  }
  span {
    font-weight: 600;
  }
}
</style>
