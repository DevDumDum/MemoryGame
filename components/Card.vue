<template>
    <div>
        <button class="pausebutton" @click="toggleTimer">Pause Game</button>
        
        <div class="timer">
            <p>Timer: {{ timer }}</p>
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
                    <div class="cardLogo" :class="item.name"></div>
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
                <div class="modal-gameover">
                    <div>
                        <div>
                            <header> 
                                <span @click="toggleTimer"></span>
                            </header>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['items'],
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

                // Player score
                score: 0

            }
        },
        mounted() {
            this.timeGenerator(); 
        },
        methods: {
            showCard(value, index){

                if(!this.firstCard){

                    this.firstCard = value
                    this.flippedCard.push(index)

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
                        }, 1000)    
                    }
                    this.firstCard = null
                    this.secondCard = null
                    
                    if(this.selectedCard.length == this.items.length / 2){

                        this.playerWon = true

                        clearInterval(this.clearTimer);
                        this.playerTime = this.timer

                        this.selectedCard = []
                    
                        this.$emit('winner', this.playerWon, this.playerTime, this.score)
                        
                        this.playerTime = null 
                        this.score = null
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
            },
        }
        
    }
</script>

<style scoped>
    .matched{ 
        text-decoration: underline;
    }

    .flipped{
        text-decoration: underline;
    }
</style>