

<template>
  <div>
    <h1 class="d-flex justify-content-center">WELCOME</h1>
    <hr />
    <div class="card" style="width: 18rem">
      <div class="card-header d-flex justify-content-center">
        <strong> {{ questions[questionIndex].title }} </strong>
      </div>
      <ul
        class="list-group list-group-flush"
        v-for="(option, index) in questions[questionIndex].options"
        :key="index"
      >
        <li
          class="list-group-item"
          @click="select(index)"
          :class="{ active: userAnswer[questionIndex] == index }"
        >
          {{ option.title }}
        </li>
      </ul>

    </div>
          <hr>
    <button class="btn btn-danger col-6 mt-5" @click="prev()">geri</button>
    <button class="btn btn-primary float-end col-6 mt-5" @click="next()">
      ileri
    </button>
    <button class="btn btn-success col-12 mt-2" @click="finishQuiz()">
      Quizi Bitir
    </button>

  <div class="mt-2" v-if="result">
        <h5 class="text-success ">Dogru Cevap : {{result}}</h5>
    <h5 class="text-danger">Yanlis Cevap : {{this.questions.length-result}}</h5>
    <h5 class="text">Toplam Soru : {{this.questions.length}}</h5>

  </div>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  name: "quiz",
  data() {
    return {
      questionIndex: 0,
      userAnswer: [],
      result: null,
      questions: [
        {
          title: "soru 1",
          options: [
            { title: "cevap 1", correct: true },
            { title: "cevap 2" },
            { title: "cevap 3" },
            { title: "cevap 4" },
            { title: "cevap 5" },
          ],
        },
        {
          title: "soru 2",
          options: [
            { title: "cevap 1" },
            { title: "cevap 2" },
            { title: "cevap 3" },
            { title: "cevap 4", correct: true },
            { title: "cevap 5" },
          ],
        },
      ],
    };
  },
  methods: {
    next() {
      if (this.questions.length > this.questionIndex) {
        this.questionIndex++;
      }
    },
    prev() {
      if (this.questionIndex !== 0) this.questionIndex--;
    },
    select(index) {
      Vue.set(this.userAnswer, this.questionIndex, index);
    },
    finishQuiz() {
      let score = 0;
      for (let i = 0; i < this.questions.length; i++) {
        if (this.questions[i].options[this.userAnswer[i]].correct) {
          score++;
        }
      }
      this.result = score;
    },
  },
};
</script>








<style scoped>
</style>