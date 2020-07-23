<template>
  <div id="app">
    <button @click="newGame()">
        NOUVELLE PARTIE
      </button>
      <hr>
      {{ score }}
      <hr>
      <div>
        <span @click='selectSquare("hautGauche")' :class="{bleu: hautGauche}" class="carre"></span>
        <span @click='selectSquare("hautDroite")' :class="{rouge: hautDroite}" class="carre"></span>
      </div>
      <div>
        <span @click='selectSquare("basGauche")' :class="{vert: basGauche}" class="carre"></span>
        <span @click='selectSquare("basDroite")' :class="{jaune: basDroite}" class="carre"></span>
      </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return{
      sequence: [],
      tmp: [],
      hautGauche: false,
      hautDroite: false,
      basGauche: false,
      basDroite: false,
      squareMapping: ["hautGauche", "hautDroite", "basGauche", "basDroite"]
    }
    },
    computed: {
      score() {
        return (this.sequence.length) ? `Score : ${this.sequence.length - 1}` : `Score : 0`;
      }
    },
     methods: {
      newGame() {
        this.allGray();
        this.sequence = [];
        this.nextTurn();
      },
      nextTurn() {
        this.addNewElemToSequence();
        this.allGray();
        this.playSequence(this.tmp[0]);
      },
      allGray() {
        this.hautGauche = false;
        this.hautDroite = false,
          this.basGauche = false,
          this.basDroite = false
      },
      selectSquare(carre) {
        if (carre === this.tmp[0]) {
           this[carre] = true;
          setTimeout(() => {
            this.allGray();
            this.tmp.shift();
            if (!this.tmp[0]) {
              this.nextTurn();
            }
          }, 400)
        } else {
          alert('Perdu!');
        }
      },
       addNewElemToSequence() {
        this.sequence.push(this.squareMapping[Math.floor(Math.random() * 4)]);
        this.tmp = this.sequence.slice();
      },
       playSequence(carre) {
        setTimeout(() => {
          this[carre] = true;
          setTimeout(() => {
            this.allGray();
            this.tmp.shift();
            if (this.tmp[0]) {
              this.playSequence(this.tmp[0]);
            } else {
              this.tmp = this.sequence.slice();
            }
          }, 400);
        }, 400);
      }
     }
 
}
</script>

<style>
  .carre { 
      display: inline-block;
         width:200px;  
          height:200px;
             background-color:#ccc;
                cursor:pointer; 
                margin: 10px;} 
 
.bleu
{
      background-color:blue; 
    } 
.rouge
 {  
      background-color:red; 
    } 
.vert 
{  
     background-color:green;
     }
 .jaune
  { 
        background-color:yellow; 
    }
</style>
