<template>
    <div>
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
                flippedCard: []
            }
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
            }
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