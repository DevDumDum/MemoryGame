<template>
    <div>
        <h1>Difficulty</h1><button @click="$emit('pageS',0)">X</button>
        <br>

                    
        <div v-if="isPlayerWon && !gameStarted">
            <h1>Time: {{ time }}</h1>
            <p>Score: {{ score }}</p>
        </div>
        <div v-else-if="!gameStarted" class="buttons">
            <button @click="setDifficulty(2, 4, 'easy')">Easy</button>
            <button @click="setDifficulty(3, 6, 'medium')">Medium</button>
            <button @click="setDifficulty(4, 8, 'hard')">Hard</button>
            <button>Custom</button>
        </div>
        <div v-else>
            <Card :items="shuffleItems" @winner="playerWon"/>
        </div>

        
    </div>
</template>

<script>
    export default {
        data(){
            return{
                easy: [
                    {name: 'APPLE', image: 'APPLE.png'},
                    
                    {name: 'BANANA', image: 'BANANA.png'},
                    {name: 'CHERRY', image: 'CHERRY.png'},
                    {name: 'GRAPES', image: 'GRAPES.png'},
                    {name: 'LEMON', image: 'LEMON.png'},
                    {name: 'ORANGE', image: 'ORANGE.png'},
                    {name: 'PEACH', image: 'PEACH.png'},
                    {name: 'WATERMELON', image: 'WATERMELON.png'}
                ],
                medium: [   
                    {name: 'BIRD', image: 'BIRD.png'},
                    {name: 'BUTTERFLY', image: 'BUTTERFLY.png'},
                    {name: 'CAT', image: 'CAT.png'},
                    {name: 'DINASOUR', image: 'DINASOUR.png'},
                    {name: 'DOG', image: 'DOG.png'},
                    {name: 'DOLPHIN', image: 'DOLPHIN.png'},
                    {name: 'DONKEY', image: 'DONKEY.png'},
                    {name: 'DUCK', image: 'DUCK.png'},
                    {name: 'EAGLE', image: 'EAGLE.png'},
                    {name: 'FISH', image: 'FISH.png'},
                    {name: 'FOX', image: 'FOX.png'},
                    {name: 'GIRAFFE', image: 'GIRAFFE.png'},
                    {name: 'HORSE', image: 'HORSE.png'},
                    {name: 'LION', image: 'LION.png'},
                    {name: 'PANDA', image: 'PANDA.png'},
                    {name: 'PARROT', image: 'PARROT.png'},
                    {name: 'PENGUIN', image: 'PENGUIN.png'},
                    {name: 'TOUCAN', image: 'TOUCAN.png'},
                ],
                hard: [

                ],
                gameStarted: false,
                randomItems: [],
                shuffleItems: [],
                size: null,

                isPlayerWon: null,
                time: null,
                score: null
        
            }
        },
        methods: {
            setDifficulty(row, col, difficulty){
                this.gameStarted = true
                this.generateRandom(row, col, difficulty)
            },
            generateRandom(row, col, difficulty){
                let tempArray = [...this[difficulty]]
                this.size = (row * col) / 2;    
                for (let i = 0; i < this.size; i++){
                    const randomIndex = Math.floor(Math.random() * tempArray.length)
                    this.randomItems.push(tempArray[randomIndex])
                    tempArray.splice(randomIndex, 1)
                }

                this.shuffleItems = [...this.randomItems, ...this.randomItems]
                this.shuffleItems.sort(() => Math.random() -0.5)
                return this.shuffleItems
            },
            playerWon(isPlayerWon, time, score){
                this.isPlayerWon = isPlayerWon
                this.time = time
                this.score = score
                this.gameStarted = false
                this.randomItems = []
                this.shuffleItems = []
                this.size = null
            }
        }
    }
</script>

<style scoped>

</style>