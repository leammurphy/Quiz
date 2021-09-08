<template>
    <div class="question-box-container">
        <b-jumbotron header="Quiz" lead="Prepare Yourself">
            <template>
                {{ currentQuestion.question }}
                some questions
            </template>
            <hr class="my-4" />
            <p>
                list of answers
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
        // mounted() {
        //     console.log(this.currentQuestion)
        // }
    }
    // any variables that we pass from App to Question, in order for it to display in the html, it must be referenced in the props
</script>
    