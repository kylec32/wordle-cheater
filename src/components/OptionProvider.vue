const wordlist = require()

<template>
  <div>
    <label for="current-status">Current Known (Use ? for unknown):</label>
    <br/>
    <input id="current-status" class="current-box" v-model="current" maxlength="5">
    <br/>
    <br/>
    <label for="known-letters">Known Letters:</label>
    <br/>
    <input id="known-letters" class="known-letters" v-model="knownLetters">
    <br/>
    <br/>
    <label for="not-included-letters">Letters Not Included:</label>
    <br/>
    <input id="not-included-letters" class="not-included-letters" v-model="notIncludedLetters">
    <br/>
    <hr/>
    <br/>
    <div class="possible-words">
        <div v-for="(word, index) in possibleWords" :key="index" class="possible-word">
            {{ word }}
        </div>
    </div>
  </div>
</template>

<script>
import possibleAnswers from './possible-answers.json'

export default {
  name: 'HelloWorld',

  data () {
    return {
      current: '',
      knownLetters: '',
      notIncludedLetters: '',
      possibleWords: []
    }
  },
  watch: {
    knownLetters: function () {
      this.processOptions()
    },
    current: function () {
      this.processOptions()
    },
    notIncludedLetters: function () {
      this.processOptions()
    }
  },
  methods: {
    processOptions: function () {
      if (this.current.length === 0) {
        return
      }
      let regularExpressionString = this.current.replace('?', '.')
      for (let i = 5 - regularExpressionString.length; i > 0; i--) {
        regularExpressionString += '.'
      }
      let regularExpression = new RegExp(regularExpressionString)
      console.log(regularExpression)
      this.possibleWords = possibleAnswers.filter((value) => {
        if (regularExpression.test(value)) {
          if (this.includesCharacters(this.knownLetters, value)) {
            return this.notIncludedLetters.length === 0 || !this.includesCharacters(this.notIncludedLetters, value)
          }
        }
        return false
      })
    },
    includesCharacters: function (charactersToInclude, targetValue) {
      // unique here would be nice
      let tempNeededCharacters = charactersToInclude.split('')
      let returnValue = true
      tempNeededCharacters.forEach((character) => {
        console.log(character)
        if (targetValue.indexOf(character) < 0) {
          console.log('false')
          returnValue = false
        }
      })

      return returnValue
    }
  }
}
</script>

<style>
input, label {
  font-size: 45px;
}
.possible-word {
    font-size: 35px;
    display: inline-block;
    width: 33%
}
</style>
