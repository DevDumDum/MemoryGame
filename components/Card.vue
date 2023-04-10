<template>
    <div>   
        <div class="timer">
            <p>Timer: {{ timer }}</p>
            <button @click="toggleTimer">{{ isTimerRunning ? 'Pause' : 'Start' }}</button>
        </div>
        <div 
            v-for="(item, index) in items"
            :key="index"
            class="card"
            :class="[{'matched' : selectedCard.includes(item.name)}, { 'flipped' : flippedCard.includes(index) }]"
            @click="showCard(item.name, index)">
            {{ index }}
            {{ item.name }}
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
                timer: '00:00',
                minutes: 0,
                seconds: 0,
                clearTimer: null,
                isTimerRunning: true
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
                        console.log("You won")
                    }
                }
                // this.selectedCard.push(value)
            },
            timeGenerator() {
                this.clearTimer = setInterval(() => {
                    this.seconds += 1;
                    if (this.seconds >= 60) {
                    this.minutes += 1;
                    this.seconds = 0;
                    }

                    let secondsValue = this.seconds < 10 ? `0${this.seconds}` : this.seconds;
                    let minutesValue = this.minutes < 10 ? `0${this.minutes}` : this.minutes; 
                    this.timer = `${minutesValue}:${secondsValue}`;
                }, 1000);
                },
                
            toggleTimer() {
            if (this.isTimerRunning) {
                clearInterval(this.clearTimer);
                this.isTimerRunning = false;
            } else {
                this.isTimerRunning = true;
                this.clearTimer = setInterval(() => {
                this.seconds += 1;
                if (this.seconds >= 60) {
                    this.minutes += 1;
                    this.seconds = 0;
                }

                let secondsValue = this.seconds < 10 ? `0${this.seconds}` : this.seconds;
                let minutesValue = this.minutes < 10 ? `0${this.minutes}` : this.minutes; 
                this.timer = `${minutesValue}:${secondsValue}`;
                }, 1000);
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