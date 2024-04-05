<template>
   <main class="container w-50 border border-primary border-5 rounded-5 my-5 p-5">
     <h3 class="text-center pb-2"> Anagram Hunt</h3>
     <div v-if="screen === 'config'" id="config-container">
        <SelectInput :options="numbers" v-model="WordLength" />
        <ol>
            <li>Choose Word Length</li>
            <li>Press <strong>Play</strong>!</li>
            <li>How many anagrams can you find in a minute?</li>
        </ol>
        <PlayButton @play-button-click="play" />
    </div>
    <div id="game-container" v-else-if="screen === 'play'">
        <div class="border-bottom row p-2 pt-4">
            <div class="col text-start fw-bold">
                <GameScore :score="score" />
            </div>
            <div class="col text-end fw-bold">
                <GameTimer :timeLeft="timeLeft" />
            </div>
        </div>
        <div>
        <AnagramsLeft :startWord="startWord" :answersLeft="answersLeft" />
        <AnswersInput v-model="answered" @change="answerChk(answered)" />
        <ol id="answer-list" class="pt-5 text-success fw-bold fs-2"></ol>
        </div>
    </div>
    <div class="text-center" id="end-game" v-else-if="screen === 'game-over'">
        <h2>Time's Up!</h2>
        <h3 class="my-4">You Got</h3>
        <p class="fs-1 fw-bold text-success">{{ finalScore }}</p>
        <p class="fs-2 fw-bold text-primary">Anagrams</p>
        <div>
         <button class="btn btn-primary form-control" @click="config()">Play Again</button>
    </div>
    </div>
   </main>
</template>

<script>   
import SelectInput from './SelectInput.vue';
import PlayButton from './PlayButton.vue';
import GameScore from './GameScore.vue';
import GameTimer from  './GameTimer.vue';
import AnagramsLeft from './AnagramsLeft';
import AnswersInput from './AnswersInput';


export default {
    name: 'MainContainer',
    components: {
        SelectInput,
        PlayButton,
        GameScore,
        GameTimer,
        AnagramsLeft,
        AnswersInput,
    },
    data: function () {
        return {
        WordLength: '',
        startArray: '',
        startWord:  '',
        randArrayIndex: '',
        randWordIndex: '',
        answered: '',
        answerKey: '',
        answersLeft: 0,
        score:  0,
        finalScore: 0,
        startTime: '',
        timeLeft: 60,
        screen: 'config',
        newAnagram: {},
        anagrams: {
            5: [
             ["abets", "baste", "betas", "beast", "beats"],
             ["acres", "cares", "races", "scare"],
             ["alert", "alter", "later"],
             ["angel", "angle", "glean"],
             ["baker", "brake", "break"],
             ["bared", "beard", "bread", "debar"],
             ["dater", "rated", "trade", "tread"],
             ["below", "bowel", "elbow"],
             ["caret", "cater", "crate", "trace", "react"],
        ],
        6:  [
           ["arrest", "rarest", "raster", "raters", "starer"],
           ["carets", "caters", "caster", "crates", "reacts", "recast", "traces"],
           ["canter", "nectar", "recant", "trance"],
           ["danger", "gander", "garden", "ranged"],
           ["daters", "trades", "treads", "stared"],
        ],
        7: [
           ["allergy", "gallery", "largely", "regally"],
           ["aspired", "despair", "diapers", "praised"],
           ["claimed", "decimal", "declaim", "medical"],
           ["dearths", "hardest", "hatreds", "threads", "trashed"],
           ["detains", "instead", "sainted", "stained"],
        ],
        8: [
           ["parroted", "predator", "prorated", "teardrop"],
           ["repaints", "painters", "pantries", "pertains"],
           ["restrain", "retrains", "strainer", "terrains", "trainers"],
           ["construe", "counters", "recounts", "trounces"],
        ],
    },
};
},
computed: {
    numbers: function () {
        const numbers = [];
        for (let number = 5; number <= 8; number++) {
            numbers.push([number, number]);
        }
        return numbers;
        },
    },
    methods: {
        config() {
            this.screen = 'config';
        },
        gameOver() {
            this.finalScore = this.score;
            this.score = 0;
            this.timeLeft = 60;
        },
        play() {
            this.screen = 'play';

            if (this.score === 0) {
                this.newAnagram = this.anagrams;
            }

            const key = this.WordLength;

            if (this.newAnagram[key].length == 0) {
                this.screen = 'game-over';
                this.gameOver();
            } else {
                this.randArrayIndex = this.getRandom(this.newAnagram[key].length);
                this.randWordIndex = this.getRandom(
                    this.newAnagram[key][this.randArrayIndex].length
                );
                this.startArray = this.newAnagram[key][this.randArrayIndex];
                this.startWord = this.newAnagram[key][this.randArrayIndex][this.randWordIndex];

                this.startArray.splice(this.randWordIndex, 1);

                this.answerKey = this.startArray;
                this.answersLeft = this.answerKey.length;
            }

            this.startTimer();
        },
     startTimer() {
      if (this.timeLeft == 60) {
        this.timer = setInterval(() => {
          this.timeLeft--;
          if (this.timeLeft === 0) {
            clearInterval(this.timer);
            this.screen = 'game-over';
            this.gameOver();
          }
        }, 1000);
      }
    },
    answerChk(answer) {
      const indexOfAnswer = this.answerKey.indexOf(answer);
      for (const i of this.answerKey) {
        if (i == answer) {
          this.score++;
          this.answered = '';
          this.answersLeft--;
          this.answerKey.splice(indexOfAnswer, 1);
          this.answerList(i);

          if (this.answerKey.length == 0) {
            const domOl = document.getElementById('answer-list');
            domOl.innerHTML = '';
            this.newAnagram[this.WordLength].splice([this.randArrayIndex], 1);
            this.play();
          }
        } else {
          this.answered = '';
        }
      }
    },
    getRandom(max) {
      return Math.floor(Math.random() * max);
    },
    answerList(text) {
      const newLiNode = document.createElement('li');
      const nodeContent = document.createTextNode(text);
      newLiNode.appendChild(nodeContent);
      const domOl = document.getElementById('answer-list');
      domOl.appendChild(newLiNode);
    },
  },
};      
</script>

<style scoped>
#main-container {
    margin: auto;
    width: 380px;
}
</style>