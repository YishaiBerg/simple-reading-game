<template>
  <q-page class="">
      <current-word v-if="currentIndex || currentIndex === 0" :word="mainData[currentIndex].word"/>
<div class="q-gutter-md row items-start q-px-sm">
            <q-img
            v-for="choice in choices"
            :key="choice"
            transition="rotate"
            :src="`statics/images/${mainData[choice].img}.jpg`"
            ratio="1"
            spinner-color="white"
            class="rounded-borders"
            @click="choiceMade(choice)"
          />
</div>
    <q-dialog
      v-model="dialog"
      persistent
      transition-show="slide-up"
      transition-hide="slide-down"
    >
    <answer-correct v-if="currentIndex === currentChoice"  @new-game="restart()"/>
    <answer-wrong v-else @close="dialog = false"/>
    </q-dialog>
    </q-page>
</template>

<script>
import CurrentWord from '../components/CurrentWord'
import AnswerCorrect from '../components/AnswerCorrect'
import AnswerWrong from '../components/AnswerWrong'

export default {
  name: 'PageIndex',
  components: {
    CurrentWord,
    AnswerCorrect,
    AnswerWrong
  },
  data () {
    return {
      currentIndex: NaN,
      choices: [],
      currentChoice: NaN,
      mainData: [
        {
          word: 'פִּיל',
          img: 'elephant'
        },
        {
          word: 'בּוֹנֶה',
          img: 'beaver'
        },
        {
          word: 'גָּמָל',
          img: 'camel'
        },
        {
          word: 'חָתוּל',
          img: 'cat'
        },
        {
          word: 'פָּרָה',
          img: 'cow'
        },
        {
          word: 'אֱיָל',
          img: 'deer'
        },
        {
          word: 'חֲמוֹר',
          img: 'donkey'
        },
        {
          word: 'גּוֹרִילָה',
          img: 'gorilla'
        },
        {
          word: 'אַרְיֵה',
          img: 'lion'
        },
        {
          word: 'כֶּבֶשׂ',
          img: 'sheep'
        },
        {
          word: 'טִיגְרִיס',
          img: 'tiger'
        }
      ],
      dialog: false
    }
  },
  methods: {
    newGame () {
      this.currentIndex = this.randIndex()
      for (let i = 0; i < 3; i++) {
        this.choices.push(this.insertUniqueChoice())
      }
      this.insertCorrectAnswer()
    },
    randIndex (len = this.mainData.length) {
      return Math.floor(Math.random() * len)
    },
    insertUniqueChoice () {
      const returnValue = this.randIndex()
      if (!this.choices.includes(returnValue) && returnValue !== this.currentIndex) {
        return returnValue
      } else return this.insertUniqueChoice()
    },
    insertCorrectAnswer () {
      this.choices.splice(this.randIndex(4), 0, this.currentIndex)
    },
    clean () {
      this.dialog = false
      this.currentIndex = NaN
      this.currentChoice = NaN
      this.choices = []
    },
    async restart () {
      this.clean()
      await this.$nextTick()
      this.newGame()
    },
    choiceMade (choice) {
      this.currentChoice = choice
      this.dialog = true
    }
  },
  mounted () {
    this.newGame()
  }
}
</script>
