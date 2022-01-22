<template>
  <div>

    <label for="current-status">Current Known (Use ? for unknown):    <svg xmlns="http://www.w3.org/2000/svg" v-show="isLoading" xmlns:xlink="http://www.w3.org/1999/xlink" style="margin:auto;" width="40px" height="40px" viewBox="0 0 100 100" preserveAspectRatio="xMidYMid">
<g transform="rotate(0 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.9166666666666666s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(30 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.8333333333333334s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(60 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.75s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(90 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.6666666666666666s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(120 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.5833333333333334s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(150 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.5s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(180 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.4166666666666667s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(210 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.3333333333333333s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(240 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.25s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(270 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.16666666666666666s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(300 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="-0.08333333333333333s" repeatCount="indefinite"></animate>
  </rect>
</g><g transform="rotate(330 50 50)">
  <rect x="47" y="24" rx="3" ry="6" width="6" height="12" fill="#000000">
    <animate attributeName="opacity" values="1;0" keyTimes="0;1" dur="1s" begin="0s" repeatCount="indefinite"></animate>
  </rect>
</g>
</svg></label>
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
    <div class="possible-words">
        <h2>Possible Answers</h2><br/>
        <div v-for="(word, index) in possibleWords" :key="index" class="possible-word">
            {{ word }}
        </div>
    </div>
    <hr/>
    <div class="possible-words">
        <h2>Possible Guesses</h2><br/>
        <div v-for="(word, index) in goodLetterGuesses" :key="index" class="possible-word">
            {{ word }}
        </div>
    </div>
  </div>
</template>

<script>
import possibleAnswers from './possible-answers.json'
import possibleWrongWords from './possible-words.json'

export default {
  name: 'HelloWorld',

  data () {
    return {
      current: '',
      knownLetters: '',
      notIncludedLetters: '',
      possibleWords: [],
      isLoading: false,
      possibleGuesses: [],
      goodLetterGuesses: []
    }
  },
  watch: {
    knownLetters: function () {
      this.runWithLoader(() => this.processOptions())
    },
    current: function () {
      this.runWithLoader(() => this.processOptions())
    },
    notIncludedLetters: function () {
      this.runWithLoader(() => this.processOptions())
    }
  },
  methods: {
    runWithLoader: function (callback) {
      this.isLoading = true
      this.possibleWords = []
      callback()
      this.calculateGoodLetterWords()
      this.isLoading = false
    },
    processOptions: function () {
      if (this.current.length === 0) {
        return
      }
      this.current.toLowerCase().replace()
      let regularExpressionString = this.current.toLowerCase().replaceAll('?', '.')
      console.log(regularExpressionString)
      for (let i = 5 - regularExpressionString.length; i > 0; i--) {
        regularExpressionString += '.'
      }
      console.log(regularExpressionString)
      let regularExpression = new RegExp(regularExpressionString)
      this.possibleWords = possibleAnswers.filter((value) => {
        if (regularExpression.test(value)) {
          if (this.includesCharacters(this.knownLetters.toLowerCase(), value)) {
            return this.notIncludedLetters.length === 0 || this.doNotIncludesCharacters(this.notIncludedLetters.toLowerCase(), value)
          }
        }
        return false
      })
    },
    includesCharacters: function (charactersToInclude, targetValue) {
      let tempNeededCharacters = charactersToInclude.split('')
      let returnValue = true
      tempNeededCharacters.forEach((character) => {
        if (targetValue.indexOf(character) < 0) {
          returnValue = false
        }
      })

      return returnValue
    },
    doNotIncludesCharacters: function (charactersToNotInclude, targetValue) {
      let tempNeededCharacters = charactersToNotInclude.split('')
      let returnValue = true
      tempNeededCharacters.forEach((character) => {
        if (targetValue.indexOf(character) >= 0) {
          returnValue = false
        }
      })

      return returnValue
    },
    calculateGoodLetterWords: function () {
      // remove words from the available answer words that include letters we know about.
      let wordsWithoutCharactersWeKnow = this.filterOutWordsWithKnownAndUnknownLetters(possibleAnswers)

      // Gather a count of each character in available answer words
      let characterMap = {}
      wordsWithoutCharactersWeKnow.forEach((value) => {
        value.split('').forEach((character) => {
          characterMap[character] = (characterMap[character] | 0) + 1
        })
      })

      // Sort the characters in order of use.
      let characterMapArray = []
      for (const character in characterMap) {
        characterMapArray.push({character: character, value: characterMap[character]})
      }
      let sortedCharacterMapArray = characterMapArray.sort((a, b) => {
        return b.value - a.value
      })

      // Assign score to each character based on how many times it appears in the available word list
      let currentScore = 26
      let scoredCharacterMap = {}
      for (let index in sortedCharacterMapArray) {
        scoredCharacterMap[sortedCharacterMapArray[index].character] = currentScore
        currentScore--
      }

      // Remove words from possible guess list that includes letters we know about.
      let guessesWithoutCharactersWeKnow = this.filterOutWordsWithKnownAndUnknownLetters(this.possibleGuesses)

      // Score each available word based on its character usage.
      let scoredWordList = guessesWithoutCharactersWeKnow.map((value) => {
        let score = 0
        let seenLetters = ''
        value.split('').forEach((character) => {
          // Don't double count scores for duplicate letters.
          if (seenLetters.indexOf(character) < 0) {
            seenLetters += character
            score += scoredCharacterMap[character]
          }
        })
        return {word: value, score: score}
      })

      // Order words by score and return the top 10.
      let orderedScoredWordList = scoredWordList.sort((a, b) => {
        return b.score - a.score
      }).map((value) => value.word)
        .slice(0, 10)

      this.goodLetterGuesses = orderedScoredWordList
    },
    filterOutWordsWithKnownAndUnknownLetters: function (words) {
      return words.filter((value) => {
        return this.doNotIncludesCharacters(this.notIncludedLetters.toLowerCase(), value) &&
            this.doNotIncludesCharacters(this.knownLetters, value) &&
            this.doNotIncludesCharacters(this.current, value)
      })
    }
  },
  created: function () {
    this.possibleGuesses.push(...possibleWrongWords)
    this.possibleGuesses.push(...possibleAnswers)
  }
}
</script>

<style>
input, label {
  font-size: 30px;
  max-width: 80%;
}
.possible-word {
    font-size: 35px;
    display: inline-block;
    width: 33%
}
</style>
