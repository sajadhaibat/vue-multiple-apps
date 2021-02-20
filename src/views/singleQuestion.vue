<template>
    <CCard>
        <CCardHeader>
            <CIcon name="cil-justify-center"/> <strong>Please Answer all Questions  <span class="float-right">Counter {{counter}}/10</span> </strong>
        </CCardHeader>

        <CCardBody>
            <CAlert class="mt-5 font-weight-bold" show color="danger" v-if="finished">You Have Successfully Finished The test, Thanks from Your time!</CAlert>
            <CJumbotron header="Bootstrap 4" lead="" v-else>

                <p class="font-lg bg-white p-2">
                    {{currentQuestion.question}}
                </p>
                <hr class="my-4">
                <CListGroup class="bg-white">
                    <CListGroupItem tag="button" class="font-weight-bold"
                                    v-for="(answer, index) in answers"
                                    :key="index"
                                   :class="answerClass(index)"
                                    @click="selectAnswer(index)"
                    >
                        {{answer}}
                    </CListGroupItem>
                </CListGroup>
                <div class="text-center mt-4">
                    <CButton  color="primary" @click="next" :disabled = "selectedIndex === null">Next</CButton>
                    <CButton color="success ml-1" @click="submitAnswer" :disabled = "selectedIndex === null">Submit</CButton>

                </div>
            </CJumbotron>
        </CCardBody>
    </CCard>
</template>

<script>
    export default {
        name: "singleQuestion",
        props: {
            currentQuestion: Object,
            next: Function,
            counter: Number,
            finished: Boolean
        },
        data(){
          return{
              selectedIndex : null,
              isActive: false,
              isCorrect : false,
              correctIndex : null,
              answered: false,
              submitted: false,
          }
        },
        computed:{
            answers() {
                this.selectedIndex = null;
                this.submitted = false;
               let answers =  [...this.currentQuestion.incorrect_answers];
               // Shuffle the answers.
               answers.splice(Math.floor(Math.random()*answers.length), 0, this.currentQuestion.correct_answer);
               this.correctIndex = answers.indexOf(this.currentQuestion.correct_answer);
                return answers;
            }
        },
        methods: {
            selectAnswer(index){
                // this.answered = false;
                this.selectedIndex = index;
                // this.isActive = true;
            },
            submitAnswer() {
                this.answered = true;
                this.submitted = true;
            },
            answerClass(index){
                let answerClass = '';
                if(this.selectedIndex === index && !this.submitted ){
                    answerClass = 'active'
                }
                else if (this.submitted && this.selectedIndex != null && this.correctIndex === index){
                 answerClass = 'correct';
                }
                else if (this.submitted && this.selectedIndex === index && this.correctIndex !== index ){
                    answerClass = 'incorrect';
                }
                return answerClass;
            }
        },

    }
</script>

<style scoped>
    .active {
    background-color: #5e36ff;
    }
    .correct {
        background-color: #269b4d;
        color: white;
    }
    .incorrect {
        background-color: #c33838;
        color: white;
    }
</style>
