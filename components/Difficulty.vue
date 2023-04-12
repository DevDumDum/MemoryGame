<template>
    <div id="mContainer">
        <div id="difficulty">
            <div>
                <img class="pausebutton" @click="toggleTimer" src="../assets/web/easy/PAUSE.png">
                <div class="timer">
                    <p>Timer: {{ timer }}</p>
                    <p>Score: {{ steps }}</p>
                </div>
                <div id="CardWrapper">
                    <div 
                        v-for="(item, index) in items"
                        :key="index"
                        class="card"
                        :class="[{'matched' : selectedCard.includes(item.name)}, { 'flipped' : flippedCard.includes(index) }]"
                        @click="showCard(item.name, index)">
                        
                        <div class="cardHidden mainCard"></div>
                        <div class="cardShown mainCard">
                            <img class="cardLogo" :class="item.name" :src="require(`@/assets/cards/easy/${item.image}`)">
                        </div>
                    </div>
                </div>

                <div v-if="pauseS" id="modalWrapper">
                    <div id="bgModal" @click="toggleTimer" ></div>
                    <div class="modal">
                        <div class="modal-content">
                            <div class="modal-image"> 
                                <div class="resume">
                                    <img src="../assets/web/paused/PAUSE.png">
                                </div>
                                <p><i>The game is paused. Click back button to resume.</i></p>
                                <div class="modal-buttons">
                                    <img class="back" src="../assets/web/paused/BACK.png" @click="toggleTimer">
                                    <!-- <img class="back" @click="toggleTimer" src="../assets/web/playisclicked/close.png"> -->
                                </div>
                            </div> 
                        </div>
                    </div>
                </div>
                
                <div v-if="isPlayerWon != null" id="modalWrapper">
                    <div id="bgModal"  @click="exit()"></div>
                    <div class="modal">
                        <div class="modal-content">
                            <div class="modal-image"> 
                                <div class="resume">
                                    <img src="../assets/web/levelcomplete/LEVEL COMPLETE.png">
                                        <h1>Time: {{ time }}</h1>
                                        <h1>Score: {{ steps }}</h1>
                                </div>
                                <div class="modal-buttons">
                                    <img class="back" src="../assets/web/gameover/EXIT.png" @click="exit()">
                                    <!-- <img class="back" @click="toggleTimer" src="../assets/web/playisclicked/close.png"> -->
                                </div>
                            </div> 
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import HighScore from './HighScore.vue';

    export default {
        props: ['items','uName'],
        //emits: ['highScore'],
        data(){
            return{
                selectedCard: [],
                firstCard: null,
                secondCard: null,
                flippedCard: [],

                // Timer Variable
                timer: '00:00:00',
                minutes: 0,
                seconds: 0,
                milliSeconds: 0,
                clearTimer: null,
                isTimerRunning: true,

                // Players time
                playerTime: null,
                pauseS: false,

                // Player score
                score: 0,

                // easy: [
                //     {name: 'APPLE', image: 'APPLE.png'},
                    
                //     {name: 'BANANA', image: 'BANANA.png'},
                //     {name: 'CHERRY', image: 'CHERRY.png'},
                //     {name: 'GRAPES', image: 'GRAPES.png'},
                //     {name: 'LEMON', image: 'LEMON.png'},
                //     {name: 'ORANGE', image: 'ORANGE.png'},
                //     {name: 'PEACH', image: 'PEACH.png'},
                //     {name: 'WATERMELON', image: 'WATERMELON.png'},
                //     {name: 'BIRD', image: 'BIRD.png'},
                //     {name: 'BUTTERFLY', image: 'BUTTERFLY.png'},
                //     {name: 'CAT', image: 'CAT.png'},
                //     {name: 'DINASOUR', image: 'DINASOUR.png'},
                //     {name: 'DOG', image: 'DOG.png'},
                //     {name: 'DOLPHIN', image: 'DOLPHIN.png'},
                //     {name: 'DONKEY', image: 'DONKEY.png'},
                //     {name: 'DUCK', image: 'DUCK.png'},
                //     {name: 'EAGLE', image: 'EAGLE.png'},
                //     {name: 'FISH', image: 'FISH.png'},
                //     {name: 'FOX', image: 'FOX.png'},
                //     {name: 'GIRAFFE', image: 'GIRAFFE.png'},
                //     {name: 'HORSE', image: 'HORSE.png'},
                //     {name: 'LION', image: 'LION.png'},
                //     {name: 'PANDA', image: 'PANDA.png'},
                //     {name: 'PARROT', image: 'PARROT.png'},
                //     {name: 'PENGUIN', image: 'PENGUIN.png'},
                //     {name: 'TOUCAN', image: 'TOUCAN.png'}
                // ]
                //gameStarted: false,
                // randomItems: [],
                // shuffleItems: [],
                size: null,

                isPlayerWon: null,
                time: null,
                score: null,
                pAgain: false,
                steps: 0,
                upScore: {
                    name: null,
                    time: null,
                    steps: null
                }
        
            }
        },
        mounted() {
            this.revealFirst();
        },
        methods: {
            // setDifficulty(row, col, difficulty){
            //     this.gameStarted = true
            //     this.generateRandom(row, col, difficulty)
            // },
            // generateRandom(row, col, difficulty){
            //     let tempArray = [...this[difficulty]]
            //     this.size = (row * col) / 2;    
            //     for (let i = 0; i < this.size; i++){
            //         const randomIndex = Math.floor(Math.random() * tempArray.length)
            //         this.randomItems.push(tempArray[randomIndex])
            //         tempArray.splice(randomIndex, 1)
            //     }
            //     this.shuffleItems = [...this.randomItems, ...this.randomItems]
            //     this.shuffleItems.sort(() => Math.random() -0.5)
            //     return this.shuffleItems
            // },
            exit(){
                this.gameStarted = false;
                this.$emit("gStatus", this.gameStarted);
            },
            revealFirst(){
                let x = 0;
                //this.toggleTimer();
                for(x; x < this.items.length; x++){
                    this.flippedCard.push(x)
                }
                setTimeout(() => {
                    this.flippedCard = []
                    //this.toggleTimer();
                    this.timeGenerator();
                }, 2000) 
            },
            playAgain(){
                this.pAgain = true;
                this.$emit("pButton", this.pAgain);
            },
            playerWonF(isPlayerWon, time, score){
                this.isPlayerWon = isPlayerWon
                this.time = time
                this.score = score
                this.gameStarted = false
                this.randomItems = []
                this.shuffleItems = []
                this.size = null
            },

            //============================================================
            showCard(value, index){
                if(!this.flippedCard.includes(index) && !this.selectedCard.includes(value) && this.flippedCard.length != 2){
                    if(!this.firstCard){

                        this.firstCard = value
                        this.flippedCard.push(index)
                        console.log(index);
                    }else if(!this.secondCard){
                        
                        this.secondCard = value
                        this.flippedCard.push(index)

                        if(this.firstCard === this.secondCard){
                            this.selectedCard.push(value) 
                            this.score += 1
                            console.log("Matched!")
                            this.flippedCard = []

                        }else{
                            console.log("Not matched!")
                            setTimeout(() => {
                                this.flippedCard = []
                            }, 500)    
                        }
                        this.steps+=1;
                        console.log(this.steps);
                        this.firstCard = null
                        this.secondCard = null
                        
                        if(this.selectedCard.length == this.items.length / 2){
                            this.playerWon = true
                            clearInterval(this.clearTimer);
                            this.playerTime = this.timer

                            this.selectedCard = []
                            this.upScore.name = this.uName;
                            this.upScore.time = this.playerTime;
                            this.upScore.steps = this.steps;

                            this.$emit("highscore", this.upScore);

                            this.playerWonF(this.playerWon, this.playerTime, this.steps);

                            //this.$emit('winner', this.playerWon, this.playerTime, this.score)
                            this.playerTime = null 
                            this.score = null
                        }
                    }
                }
                // this.selectedCard.push(value)
            },
            timeGenerator() {
                this.clearTimer = setInterval(() => {

                    this.milliSeconds += 10; 

                    if (this.milliSeconds >= 1000) {
                        this.seconds += 1;
                        this.milliSeconds = 0;
                    }

                    if (this.seconds >= 60) {
                    this.minutes += 1;
                    this.seconds = 0;
                    }

                    let milliSecondsValue = `${this.milliSeconds / 10}`

                    let secondsValue = this.seconds < 10 ? `0${this.seconds}` : this.seconds
                    let minutesValue = this.minutes < 10 ? `0${this.minutes}` : this.minutes 
                    this.timer = `${minutesValue}:${secondsValue}:${milliSecondsValue}`
                }, 10);
            },

            toggleTimer() {
                if (this.isTimerRunning) {
                clearInterval(this.clearTimer);
                this.isTimerRunning = false;
                this.pauseS = true;
                } else {
                this.isTimerRunning = true;
                this.clearTimer = setInterval(() => {

                this.milliSeconds += 10; 

                if (this.milliSeconds >= 1000) {
                    this.seconds += 1;
                    this.milliSeconds = 0;
                }

                if (this.seconds >= 60) {
                this.minutes += 1;
                this.seconds = 0;
                }

                let milliSecondsValue = `${this.milliSeconds / 10}`

                let secondsValue = this.seconds < 10 ? `0${this.seconds}` : this.seconds
                let minutesValue = this.minutes < 10 ? `0${this.minutes}` : this.minutes 
                this.timer = `${minutesValue}:${secondsValue}:${milliSecondsValue}`
                }, 10);
                this.pauseS = false;
                }
            }
        }
    }
</script>

<!-- <style>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
}

.modal-buttons {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}
</style> -->
