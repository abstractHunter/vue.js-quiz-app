<template>
  <section>
    <h2>{{ category.name }}</h2>
    <QuestionComponent
      :question="currentQuestion"
      :showAnswers="showAnswers"
      :selectedProposalFromParent="selectedProposals[currentIndex]"
      @previousQuestion="previousQuestion"
      @nextQuestion="nextQuestion"
    />
    <button v-if="canTerminate" @click="terminate">Terminer</button>
  </section>
</template>

<style>
section {
  display: flex;
  flex-direction: column;
  align-items: center;
}
button {
  margin-top: 1rem;
  width: 120px;
  height: 40px;
  border: 2px solid rgb(20, 100, 220);
  border-radius: 5px;
  background-color: rgb(20, 100, 220, 0.3);
  cursor: pointer;
}
button:hover {
  background-color: rgb(20, 100, 220, 0.5);
}
</style>

<script>
import sourceData from "@/data.json";
import QuestionComponent from "@/components/QuestionComponent.vue";

export default {
  name: "QuizView",

  components: {
    QuestionComponent,
  },

  data() {
    return {
      currentIndex: 1,
      showAnswers: false,
      selectedProposals: {},
    };
  },

  methods: {
    nextQuestion(selectedProposal) {
      if (selectedProposal !== null) {
        this.selectedProposals[this.currentIndex] = selectedProposal;
      }
      if (this.selectedProposals.length === this.category.questions.length) {
        this.canTerminate = true;
      } else if (this.currentIndex < this.category.questions.length) {
        this.currentIndex++;
      }
    },
    previousQuestion(selectedProposal) {
      if (selectedProposal !== null) {
        this.selectedProposals[this.currentIndex] = selectedProposal;
      }
      if (this.currentIndex > 1) {
        this.currentIndex--;
      }
    },
    terminate() {
      this.showAnswers = true;
    },
  },

  computed: {
    category() {
      return sourceData.categories.find(
        (category) => category.slug === this.$route.params.slug
      );
    },
    currentQuestion() {
      return this.category.questions.find(
        (question) => question.id === this.currentIndex
      );
    },
    canTerminate() {
      return (
        Object.keys(this.selectedProposals).length ===
        this.category.questions.length
      );
    },
  },
};
</script>
