<template>
<div>

    <CRow>
        <CCol class="col-md-8 offset-md-2" >
            <singleQuestion
                    v-if="questions.length"
                    :current-question="questions[index]"
                    :next="next"
                    :counter = "counter"
                    :finished = "quizFinished"
            ></singleQuestion>
        </CCol>
    </CRow>
</div>
</template>

<script>
    import axios from 'axios';
    import singleQuestion from "./singleQuestion";
    export default {
        name: "askQuestions",
        components: {
            singleQuestion
        },
        data(){
          return {
              questions: [],
              index: 0,
              counter: 1,
              quizFinished: false
          }
        },
        methods:{
          next(){
              this.counter++;

              if (this.counter === 10) {
                  this.quizFinished = true;
                  return
              }
              this.index++;
          }
        },
        mounted() {
            axios.get('https://opentdb.com/api.php?amount=10&category=18&type=multiple')
                .then(response =>
                    // console.log(JSON.stringify(response.data.results)));
                    (this.questions = response.data.results));
        }
    }
</script>

<style scoped>

</style>
