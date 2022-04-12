<template>
  <div class="card-container">
    <div class="card-wrapper">
      <span v-if="advice">ADVICE #{{ advice.id }}</span>
      <h2 v-if="advice">{{ advice.advice }}</h2>
      <img
        src="../assets/pattern-divider-desktop.svg"
        alt="horizontal-line"
        class="horizontal-line"
      />
      <div v-on:click="getNewAdvice" class="dice-container">
        <img
          v-on:click="getNewAdvice"
          src="../assets/icon-dice.svg"
          alt="icon-dice"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { IAdviceProps } from "../types";
import axios from "axios";

@Component
export default class Card extends Vue {
  advice: IAdviceProps = {
    advice: "Loading...",
  };

  async getNewAdvice(): null {
    this.advice.advice = "Loading...";
    const response = await axios.get("https://api.adviceslip.com/advice");
    this.advice = response.data.slip;
  }

  async created(): null {
    this.getNewAdvice();
  }
}
</script>

<style scoped lang="scss">
.card-container {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;

  .card-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    flex-direction: column;
    max-width: 560px;
    padding: 3rem;
    background-color: hsl(217, 19%, 24%);
    color: white;
    border-radius: 15px;

    span {
      margin-bottom: 1.5rem;
      letter-spacing: 0.3rem;
      color: hsl(150, 100%, 66%);
      font-size: 14px;
    }

    h2 {
      text-align: center;
      font-size: 28px;
      font-weight: 800;
    }

    .horizontal-line {
      margin: 2rem 0 1.5rem 0;
    }

    .dice-container {
      position: absolute;
      width: 60px;
      height: 60px;
      background-color: hsl(150, 100%, 66%);
      border-radius: 50%;
      bottom: -18px;
      transform: translateY(18%);
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
    }
  }
}

@media (max-width: 375px) {
  .card-container {
    .card-wrapper {
      max-width: 350px;
    }
  }
}
</style>
