<template>
  <div
    class="proposal"
    @click="select"
    :class="{
      'selected-proposal': selected,
      'correct-proposal': isCorrect,
      'incorrect-proposal': isIncorrect,
    }"
  >
    {{ name }}
  </div>
</template>

<style>
.proposal {
  margin: 0.8rem;
  padding: 1rem;
  border: 2px solid #aaa;
  border-radius: 5px;
  cursor: pointer;
  width: 280px;
  background-color: rgba(170, 170, 170, 0.3);
}
.proposal:hover {
  background-color: rgba(170, 170, 170, 0.5);
}
.selected-proposal {
  border: 2px solid rgb(20, 100, 220);
  background-color: rgb(20, 100, 220, 0.3);
}
.correct-proposal {
  border: 2px solid rgb(80, 220, 80);
  background-color: rgba(80, 220, 80, 0.3);
}
.incorrect-proposal {
  border: 2px solid rgb(220, 80, 80);
  background-color: rgba(220, 80, 80, 0.3);
}
</style>

<script>
export default {
  name: "QuestionProposalComponent",

  props: {
    name: { type: String, required: true },
    selected: { type: Boolean, default: false },
    isCorrect: { type: Boolean, default: false },
    isIncorrect: { type: Boolean, default: false },
  },

  methods: {
    select() {
      this.$emit("select", this.name);
    },
  },
};
</script>
