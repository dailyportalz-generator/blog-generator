<template>
  <div class="blog-koushin-result">
    <div class="blog-koushin-result_main">
      <img src="@/assets/waku_up.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/waku_left.gif" alt>
        <div class="blog-koushin-result__message">
          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber" :key="questionNumber">
              <template v-if="questionNumber === 5">
                <img :src="imgList[questions.q6-1]" />
                <br>
              </template>
              <template v-for="(result, resultIndex) in results">
                <span :key="result" v-if="questions[`q${questionNumber+1}`] === resultIndex+1">{{result}}</span>
              </template>
            </p>
          </template>
        </div>
        <img src="@/assets/waku_left.gif" alt>
      </div>
      <img src="@/assets/waku_down.gif" alt>
    </div>
    <template v-if="step >= 6">
      <p class="oyasumi-result_build">
        <button type="button" @click="handleClickRestart">もう一度つくる</button>
      </p>
      <p class="oyasumi-result_share">
        <input type="text" class="oyasumi-result_shareurl" readonly :value="shareUrl">
        <a target="_blank" :href="twitterUrl">つぶやく</a>
      </p>
    </template>
  </div>
</template>

<script>
import { stringify } from 'querystring'
export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    resultsList() {
      return [
        [
          'たびたびこんにちは。更新ばかりしているけど、暇じゃないんですよ。',
          'いやっほう！ 寝る前にブログを更新するのが日課になりつつあります…。',
          '数えてみたら更新したのがちょうど先週の今日。あっというまですねー…こうやって年をとってゆくのでしょうか。',
          '生きてきょうもおきたら午後でした。流れ行く雲をぼんやり見たり、雲の種類をネットで調べたりしてました。います。本業のほうが忙しくてブログのほうをかまけておりました。これからは毎日更新します。'
        ],
        [
          'またデザインを変更してみました。スタイルシートも変更したので少しは見やすくなったかなと思います。',
          '今日はちょっとまじめな話をしようと思います。みなさんも新聞やニュースで目にしているあの出来事についてです。',
          '去年の暮れから盛り上がっているハバロフクステクノシーンの重鎮「赤い鋼鉄」の新譜をゲットしましたー。',
          'きょうもおきたら午後でした。流れ行く雲をぼんやり見たり、雲の種類をネットで調べたりしてました。'
        ],
        [
          'それに関して驚きの情報を入手しました。ちょっとここには書けないのですが、いやあ、まさかナニがアレとは…。',
          '本当はほかにやらなきゃいけないことがたくさんあるのですが。ついつい誘惑に負けてしまい…。弱い生き物です。',
          'なんというかですね。うまく言えないのですが、やっぱり毎日が勝負だなと思うわけです。',
          'そしたら、なんだかじゅんとしてきちゃたんです。'
        ],
        [
          'みなさんもどうでしょうか。オススメです。メッセでトラバでアフリエートよろしく。',
          '私って見かけによらずついつい考えすぎてしまうので。しかもたいていは悪い方向にばかり。',
          'やっぱり21世紀は心の時代だな、唐突にそんなことを思いました。できることからはじめてゆきたいです。',
          '♪ けさ君の夢を見た。君が蛇口になってる夢を。その蛇口からは何が出る？　by ブッセ'
        ],
        [
          'と、そんな感じで生きております。',
          'お風呂はいるのでこの辺りで。オイオイ。',
          'この年になってこんなことを言っているのはいかがなものかと思いますが！',
          'あ、そうそう。K ちゃん、来週のことで話したいので連絡よろしく！'
        ],
        [
          '↑私の気持ち',
          '↑もらいものです',
          '↑写真と本文は関係ありません',
          '↑今日のランチ'
        ]
      ]
    },
    imgList() {
      return [
        require('@/assets/p01.jpg'),
        require('@/assets/p02.jpg'),
        require('@/assets/p03.jpg'),
        require('@/assets/p04.jpg')
      ]
    },
    shareUrl() {
      const shareData = {
        ...this.questions.target,
        ...this.questions,
        target: null,
        share: 1
      }
      delete shareData.target
      return `https://dailyportalz.jp/kiji/blog-koushin-generator?${stringify(
        shareData
      )}`
    },
    twitterUrl() {
      return `https://twitter.com/intent/tweet?text=ブログ更新ジェネレーター&url=${encodeURIComponent(
        this.shareUrl
      )}`
    }
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}
.blog-koushin-result {
  width: 526px;
  margin: 0 auto;
}
.blog-koushin-result_main {
  font-size: 0;
}
.blog-koushin-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}
.blog-koushin-result__message p:first-child {
  margin-top: 0;
}
.blog-koushin-result_build {
  text-align: right;
}
.blog-koushin-result_share {
  font-size: 12px;
}
.blog-koushin-result_shareurl {
  width: 100%;
}
.blog-koushin-result_share {
  display: flex;
  align-items: center;
}
input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>