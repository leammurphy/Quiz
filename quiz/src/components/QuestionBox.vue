<template>
    <div class="question-box-container">
        <b-jumbotron header="Quiz" lead="Prepare Yourself">
            <template>
                {{ currentQuestion.question }}
            </template>
            <hr class="my-4" />

                <b-list-group>
                    <b-list-group-item 
                        v-for="(answer, index) in answers" 
                        :key="index"
                        @click="selectAnswer(index)"
                        :class="answerClass(index)"
                    >
                        
                        {{answer}}
                        
                     </b-list-group-item>

                </b-list-group>


            <b-button 
                variant="primary"
                @click="submitAnswer"
                :disabled="selectedIndex === null || answered"
            >
                Submit
            </b-button>
            <b-button @click ="next" variant="success">Next</b-button>
        </b-jumbotron>
    </div>     
</template>

<script>
    import _ from 'lodash'
    export default {
        props: {
            currentQuestion: Object,
            next: Function, 
            increment: Function,
        },
        data() {
            return {
                selectedIndex: null,
                correctIndex: null,
                shuffledAnswers: [],
                answered: false
            }
        },
        computed: {
            answers() {
               let answers =  [...this.currentQuestion.incorrect_answers]
               answers.push(this.currentQuestion.correct_answer)
               return answers
            }
        },
        methods: {
            selectAnswer(index) {
                this.selectedIndex = index
                console.log(index)
            },
            shuffleAnswers() {
                let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
                this.shuffledAnswers = _.shuffle(answers)
                this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
            },
            submitAnswer() {
                let isCorrect = false

                if (this.selectedIndex === this.correctIndex) {
                    isCorrect = true
                }
                this.answered = true

                this.increment(isCorrect)
            },
            answerClass(index) {
                let answerClass = ''

                if (!this.answered && this.selectedIndex === index) {
                    answerClass = 'selected'
                } else if (this.answered && this.correctIndex === index) {
                    answerClass = 'correct'
                } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
                    answerClass = 'incorrect'
                }

                return answerClass
            }
        },
        watch: {
            currentQuestion: {
                immediate: true,
                handler() {
                    this.selectedIndex = null
                    this.answered = false
                    this.shuffleAnswers()
                }
            }
            
        },
        mounted() {
            this.shuffleAnswers()
        }
    }
    // any variables that we pass from App to Question, in order for it to display in the html, it must be referenced in the props
</script>
    

<style scoped> 
/* These are the styles */
    .list-group {
        margin-bottom: 15px;
    }
    .list-group-item:hover {
        background: #EEE;
        cursor: pointer;
    }
    .btn {
        margin: 0 5px;
    }
    .selected {
        background-color: lightblue;
    }
    .correct {
        background-color:lightgreen;
    }
    .incorrect {
        background-color: lightcoral;
    }
</style>