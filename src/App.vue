<template>
  <div id="app">
    <template>
      <span v-if="step < 6"><b>step{{step+1}}</b></span>
      <SelectQuestion
        key="start"
        v-if="step === 0"
        v-model="questions.q1"
        @next="handleNext"
        :message="messageList[0]"
        :choices="choicesList[0]"
      />

      <SelectQuestion
        key="question2"
        v-if="step === 1"
        v-model="questions.q2"
        @next="handleNext"
        :message="messageList[1]"
        :choices="choicesList[1]"
      />

      <SelectQuestion
        key="question3"
        v-if="step === 2"
        v-model="questions.q3"
        @next="handleNext"
        :message="messageList[2]"
        :choices="choicesList[2]"
      />

      <SelectQuestion
        key="question4"
        v-if="step === 3"
        v-model="questions.q4"
        @next="handleNext"
        :message="messageList[3]"
        :choices="choicesList[3]"
      />

      <SelectQuestion
        key="question5"
        v-if="step === 4"
        v-model="questions.q5"
        @next="handleNext"
        :message="messageList[4]"
        :choices="choicesList[4]"
      />

      <SelectQuestion
        key="question6"
        v-if="step === 5"
        v-model="questions.q6"
        @next="handleNext"
        :message="messageList[5]"
        :choices="choicesList[5]"
      />
    </template>

    <BlogKoushinResult
      :step="step"
      :questions="questions"
    />
  </div>
</template>

<script>
import SelectQuestion from './components/SelectQuestion.vue'
import BlogKoushinResult from './components/BlogKoushinResult.vue'
import { parse } from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      step: 0,
      questions: {
        name: '',
        title: 1,
        q1: 1,
        q2: 1,
        q3: 1,
        q4: 1,
        q5: 1,
        q6: 1,
      }
    }
  },
  components: {
    SelectQuestion,
    BlogKoushinResult
  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = ['name', 'title', 'q1', 'q2', 'q3', 'q4', 'q5', 'q6'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (val != 'name' && parseInt(params[val]) < 1) {
        return false
      }
      return true
    })
    if (isValid) {
      const questions = {
        name: params.name,
        title: parseInt(params.title),
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5),
        q6: parseInt(params.q6)
      }
      this.questions = questions
      this.step = 7
    }
  },
  methods: {
    handleNext() {
      this.step ++
    }
  },
  computed: {
    messageList() {
      return [
        '前回更新したのはいつですか？',
        'さて、なにについて書こうか',
        'どうつなげますか',
        'しめにむけて',
        'どう落とす？',
        '写真でも入れてごまかしとこう',
      ]
    },
    choicesList() {
      return [
        ['今日', '昨日', '一週間ぶり', '一ヶ月以上前'],
        ['このブログについて', '政治のこと', '音楽のこと', 'なにもない'],
        ['驚きでひきつける', 'しっとりと', 'ポジティブに', '宇能鴻一郎風に'],
        ['いきおいだけで', '自意識過剰に', 'まじめに', 'ポエムでごまかす'],
        ['丁寧だけど何も言わずに', '現実に戻る', '自虐トーンで', '私信で'],
        ['心象風景', 'おもしろ', '写真と本文は関係ありません', 'ごはん']
      ]
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>