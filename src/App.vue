<template>
  <div id="app">
  <h1>Hangman! </h1>
    <div>
      <div>
         Lives left : {{ lives}}
      </div>
      <div class="button" v-for="item in this.alphabet">
          <button v-on:click="click(item.letter), checkStatus()"> {{ item.letter }} </button>
      </div>
    </div>   
    Selected Letters : 
    <div class="letter" v-for="item in selectedLetters">
      {{ item }}
    </div>
    <div>
      Word to guess : 
      <div class="letter" v-for="letter in randomWord.toUpperCase()">
        <h1 v-if="selectedLetters.includes(letter)">{{ letter }}</h1>
        <h1 v-else>_</h1>   
      </div>
    </div>    
  </div>
</template>

<script>

export default {
  data: function () { 
    return {
      lives: 5,
      total: 0,
      randomWord : '',
      wordList : [
        "locomotive",
        "television",
        "manequin",
        "livre",
        "cercueil",
        "cyclope",
      ],
      selectedLetters: [],
      alphabet: [
        { letter: 'A' },
        { letter: 'B' },
        { letter: 'C' },
        { letter: 'D' },
        { letter: 'E' },
        { letter: 'F' },
        { letter: 'G' },
        { letter: 'H' },
        { letter: 'I' },
        { letter: 'J' },
        { letter: 'K' },
        { letter: 'L' },
        { letter: 'M' },
        { letter: 'N' },
        { letter: 'O' },
        { letter: 'P' },
        { letter: 'Q' },
        { letter: 'R' },
        { letter: 'S' },
        { letter: 'T' },
        { letter: 'U' },
        { letter: 'V' },
        { letter: 'W'},
        { letter: 'X' },
        { letter: 'Y' },
        { letter: 'Z' },
      ],
    };
  },
  methods: {
    click: function (char) {
      if((!(this.randomWord.toUpperCase().includes(char))) && !this.selectedLetters.includes(char)){
        this.lives -= 1;
        this.selectedLetters.push(char)
      } else if(this.randomWord.toUpperCase().includes(char) && !this.selectedLetters.includes(char)){
        this.selectedLetters.push(char)
        this.total += 1;
      }
      
    },
    checkStatus: function(){
      if(this.lives <= 0){
        alert("You lost! Reload to restart.")
      } else if(this.total == this.randomWord.length){
        alert("You win!")
      }
      
    }
  },

  created (){
    this.randomWord =  this.wordList[Math.floor(Math.random() * this.wordList.length)]
  },
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.button {
  height: 2em;
  width: 2em;
  padding: 0.2em;
  display: inline-block;
}
.letter {
  height: 2em;
  width: 2em;
  padding: 0.2em;
  display: inline-block;
}
</style>
