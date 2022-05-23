<template>
  <div class="wizard-page flex justify-center rounded shadow-lg">
    <template v-if="currentPage === 2">
      <div class="form w-3/4 shadow-lg">
        <h2 class="header-text">Tell us about Yourself</h2>

        <form class="form-groups">
          <div class="form-input w-2/5">
            <label>Name</label>
            <input type="text" v-model="userDetails.name" />
          </div>

          <div class="form-input w-2/5">
            <label>Age</label>
            <input type="number" v-model="userDetails.age" min="0" />
          </div>

          <div class="form-input w-2/5">
            <label>Where do you live?</label>
            <select v-model="userDetails.country">
              <option value="Hongkong">Hong Kong</option>
              <option value="USA">USA</option>
              <option value="Australia">Australia</option>
            </select>
          </div>
        </form>

        <template v-if="userDetails.age && userDetails.country">
          <h2 class="mt-3 font-bold package-header">Choose Your Package</h2>
          <div class="cards w-full">
            <div
              class="card rounded shadow-lg w-1/3"
              @click="selectedPremium = 'standard'"
              :class="{ 'card-active': selectedPremium === 'standard' }"
            >
              <h2>Standard</h2>
              <h4>{{ rates?.standard || "" }}</h4>
            </div>

            <div
              class="card rounded shadow-lg w-1/3"
              @click="selectedPremium = 'safe'"
              :class="{ 'card-active': selectedPremium === 'safe' }"
            >
              <h2>Safe</h2>
              <h4>{{ rates?.safe || "" }}</h4>
              <p>( Standard + 50% )</p>
            </div>

            <div
              class="card rounded shadow-lg w-1/3"
              @click="selectedPremium = 'superSafe'"
              :class="{ 'card-active': selectedPremium === 'superSafe' }"
            >
              <h2>Super Safe</h2>
              <h4>{{ rates?.superSafe || "" }}</h4>
              <p>( Standard + 75% )</p>
            </div>
          </div>
        </template>
      </div>

      <ShortSummary
        :premiumRate="rates[selectedPremium]"
        :userDetails="userDetails"
        @goNext="goNext()"
      />
    </template>
    <template v-if="currentPage === 3">
      <FinalSummary
        @goBack="currentPage = 2"
        :premiumRate="rates[selectedPremium]"
        :userDetails="userDetails"
        :selectedPremium="selectedPremium"
      />
    </template>

    <template v-if="currentPage === -1">
      <PageError />
    </template>
  </div>
</template>

<script>
import ShortSummary from "@/components/ShortSummary";
import FinalSummary from "@/components/FinalSummary";
import PageError from "@/components/PageError";
import { ratePerCountry, currency } from "../helpers/constants.js";

export default {
  name: "WizardView",
  data() {
    return {
      userDetails: {
        name: "",
        age: "",
        country: "",
      },
      selectedPremium: "standard",
      rates: {},
      currentPage: 2,
    };
  },
  components: { ShortSummary, FinalSummary, PageError },
  methods: {
    goNext() {
      if (this.userDetails.age > 100) {
        this.currentPage = -1;
      } else {
        this.currentPage = 3;
      }
    },
  },
  watch: {
    userDetails: {
      deep: true,
      handler(val) {
        if (!(val.age && val.country)) return;
        this.rates = {
          standard:
            10 * val.age * ratePerCountry[val.country] +
            " " +
            currency[val.country],
          safe:
            10 * val.age * ratePerCountry[val.country] * 1.5 +
            " " +
            currency[val.country],
          superSafe:
            10 * val.age * ratePerCountry[val.country] * 1.75 +
            " " +
            currency[val.country],
        };
      },
    },
  },
};
</script>

<style scoped lang="scss">
.wizard-page {
  padding: 50px;
  display: flex;
  justify-content: center;
}

.form {
  padding: 50px;
  background: #0b4141;
  color: #faf0dc;
}

.header-text {
  font-size: 2rem;
}

.form-groups {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.form-input {
  display: flex;
  flex-direction: column;
  text-align: left;
  margin: 10px;
  input,
  select {
    padding: 5px;
    color: black !important;
  }
}

.package-header {
  border-top: 2px solid silver;
}

.cards {
  display: flex;

  .card {
    padding: 20px;
    margin: 24px;
    background: #0f2557;
    color: #faf0dc;

    h2 {
      font-size: 1.5rem;
      font-weight: bold;
    }
  }
  .card:hover {
    transform: scale(1.1);
  }

  .card-active {
    box-shadow: 0px 0px 12px 2px #ff6864;
    -webkit-box-shadow: 0px 0px 12px 2px #ff6864;
    -moz-box-shadow: 0px 0px 12px 2px #ff6864;
  }
}
</style>
