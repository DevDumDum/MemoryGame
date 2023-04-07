<template>
    <div>
        <h1>Difficulty</h1><button @click="$emit('pageS',0)">X</button>
        <br>
        <div v-if="!gameStarted"  class="buttons">
            <button @click="setDifficulty(2, 4)">Easy</button>
            <button @click="setDifficulty(3, 6)">Medium</button>
            <button @click="setDifficulty(4, 8)">Hard</button>
            <button>Custom</button>
        </div>

        <div v-else>
            <Card :items="shuffleItems"/>
        </div>

        
    </div>
</template>

<script>
    export default {
        data(){
            return{
                items: [
                    {name: 'APPLE', image: 'APPLE.png'},
                    {name: 'BANANA', image: 'BANANA.png'},
                    {name: 'CHERRY', image: 'CHERRY.png'},
                    {name: 'GRAPES', image: 'GRAPES.png'},
                    {name: 'LEMON', image: 'LEMON.png'},
                    {name: 'ORANGE', image: 'ORANGE.png'},
                    {name: 'PEACH', image: 'PEACH.png'},
                    {name: 'WATERMELON', image: 'WATERMELON.png'}
                ],
                gameStarted: false,
                randomItems: [],
                shuffleItems: []
            }
        },
        methods: {
            setDifficulty(row, col){
                this.gameStarted = true
                this.generateRandom(row, col)
            },
            generateRandom(row, col){
                let tempArray = [...this.items]
                this.size = (row * col) / 2;    
                for (let i = 0; i < this.size; i++){
                    const randomIndex = Math.floor(Math.random() * tempArray.length)
                    this.randomItems.push(tempArray[randomIndex])
                    tempArray.splice(randomIndex, 1)
                }

                this.shuffleItems = [...this.randomItems, ...this.randomItems]
                this.shuffleItems.sort(() => Math.random() -0.5)
                return this.shuffleItems
            }
        }
    }
</script>

<style scoped>

</style>