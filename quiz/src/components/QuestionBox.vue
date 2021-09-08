<template>
    <div class="question-box-container">
        <b-jumbotron header="Quiz" lead="Prepare Yourself">
            <template>
                {{ currentQuestion.question }}
            </template>
            <hr class="my-4" />
            <p  v-for="(answer, index) in answers" :key="index">
               {{answer}}
            </p>
            <b-button variant="primary" href="#">Submit</b-button>
            <b-button @click ="next" variant="success" href="#">Next</b-button>
        </b-jumbotron>
    </div>     
</template>

<script>
    export default {
        props: {
            currentQuestion: Object,
            next: Function, 
        },
        computed: {
            answers() {
               let answers =  [...this.currentQuestion.incorrect_answers]
               answers.push(this.currentQuestion.correct_answer)
               return answers
            }
        }


        // mounted() {
        //     console.log(this.currentQuestion)
        // }
    }
    // any variables that we pass from App to Question, in order for it to display in the html, it must be referenced in the props
</script>
    