<template>
  <div>
    <ol>
      <TodoItem v-for="todo in todos" :key="todo.id" :item="todo"></TodoItem>
    </ol>
    <br />
    <hr />
    <br />
    <p>
      Ask a yes/no question:
      <input v-model="question" />
    </p>
    <p>{{ answer }}</p>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
import _ from 'lodash'
import axios from 'axios'

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      question: '',
      answer: 'I cannot give you an answer until you ask a question!',
      todos: [
        { id: 1, text: 'Vue Js' },
        { id: 2, text: 'Angular' },
        { id: 3, text: 'React' },
      ],
    }
  },
  watch: {
    question(newQuestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      this.debouncedGetAnswer()
    },
  },
  created() {
    this.debouncedGetAnswer = _.debounce(this.getAnswer, 500)
  },
  methods: {
    getAnswer() {
      if (!this.question.includes('?')) {
        this.answer = 'Questions usually contain a question mark. ;-)'
        return
      }
      this.answer = 'Thinking...'
      const vm = this
      axios
        .get('https://yesno.wtf/api')
        .then(function (response) {
          vm.answer = _.capitalize(response.data.answer)
        })
        .catch(function (error) {
          vm.answer = 'Error! Could not reach the API. ' + error
        })
    },
  },
}
</script>

<style></style>
