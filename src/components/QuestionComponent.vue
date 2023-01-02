<template>
  <div class="question-container">
    <h3>{{ question.question }}</h3>
    <div v-if="showAnswers">
      <QuestionProposalComponent
        v-for="proposal in question.proposals"
        :key="proposal"
        :name="proposal"
        :isCorrect="proposal === question.answer"
        :isIncorrect="
          proposal === getSelectedProposal && proposal !== question.answer
        "
      />
    </div>
    <div v-else>
      <QuestionProposalComponent
        v-for="proposal in question.proposals"
        :key="proposal"
        :name="proposal"
        :selected="proposal === getSelectedProposal"
        @select="selectProposal"
      />
    </div>
    <div class="buttons">
      <button @click="previousQuestion">Previous</button>
      <button @click="nextQuestion">Next</button>
    </div>
  </div>
</template>

<style>
.question-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.buttons {
  margin-top: 0.7rem;
  display: flex;
  justify-content: space-between;
  width: 320px;
}

.buttons button {
  width: 120px;
  height: 40px;
  border: 2px solid rgb(220, 200, 20);
  border-radius: 5px;
  background-color: rgba(220, 200, 20, 0.3);
  cursor: pointer;
}
.buttons button:hover {
  background-color: rgba(220, 200, 20, 0.5);
}
</style>

<script>
import QuestionProposalComponent from "@/components/QuestionProposalComponent.vue";

export default {
  name: "QuestionComponent",

  components: {
    QuestionProposalComponent,
  },

  props: {
    question: { type: Object, required: true },
    showAnswers: { type: Boolean, default: false },
    selectedProposalFromParent: { type: String, default: null },
  },

  data() {
    return {
      selectedProposal: null,
    };
  },

  computed: {
    getSelectedProposal() {
      return this.selectedProposal || this.selectedProposalFromParent || null;
    },
  },

  methods: {
    selectProposal(proposal) {
      this.selectedProposal = proposal;
    },
    previousQuestion() {
      this.$emit("previous-question", this.selectedProposal);
      this.selectedProposal = null;
    },
    nextQuestion() {
      this.$emit("next-question", this.selectedProposal);
      this.selectedProposal = null;
    },
  },
};
</script>
