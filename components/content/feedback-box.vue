<script setup lang="ts">
import { ref } from "vue";

const isSubmitted = ref(false);
const { submitFeedback } = useDocusFeedback()

const feedbackOptions = [
  {
    title: "Worst Doc ever 🥲",
    value: 1,
  },
  {
    title: "Not helpful 🤬",
    value: 2,
  },
  {
    title: "Helpful 😊",
    value: 3,
  },
  {
    title: "Super Helpful 😍",
    value: 4,
  },
];

function giveFeedback(title: string) {
  submitFeedback(title);
  isSubmitted.value = true;
}
</script>

<template>
  <div class="feedback-box-wrapper">
    <div v-if="!isSubmitted">
      <p>What do you think?</p>
      <h2>How helpful was this article?</h2>
      <div class="feedback-box-list">
        <template v-for="feedbackOption of feedbackOptions" :key="feedbackOption.value">
          <div
            class="feedback-box-item" @click="giveFeedback(feedbackOption.title)"
          >
            <h3>{{ feedbackOption.title }}</h3>
          </div>
        </template>
      </div>
    </div>
    <div v-else class="transition-opacity">
      <h2>Thank you for your feedback!</h2>
    </div>
  </div>
</template>

<style scoped>
.feedback-box-wrapper {
  display: flex;
  justify-content: start;
  flex-direction: column;
  text-align: start;
  padding: 1rem;
  border: 2px #f8a000cc dashed;
  border-radius: 5px;
}

p {
  color: gray;
  font-size: 1rem;
}

h2 {
  font-size: 1.2rem;
  font-weight: bold;
}

.feedback-box-list {
  display: flex;
  justify-content: start;
  flex-direction: row;
  margin-top: 1rem;
}

.feedback-box-item {
  padding: 0.3rem 0.5rem;
  border: 2px #3c3c3c6c solid;
  border-radius: 10px;
  margin-right: 0.8rem;
}

.feedback-box-item:hover {
  cursor: pointer;
  background-color: #f8a000;
  color: black;
}

</style>
