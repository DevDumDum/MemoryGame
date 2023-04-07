<template>
    <div>
        <div 
            v-for="(item, index) in items"
            :key="index"
            class="card"
            :class="{'matched' : selectedCard.includes(item.name)}"
            @click="showCard(item.name)">
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
                secondCard: null
            }
        },
        methods: {
            showCard(value){
                if(!this.firstCard){
                    this.firstCard = value
                }else{
                    this.secondCard = value
                    if(this.firstCard == this.secondCard){
                        this.selectedCard.push(value)
                        console.log("Matched!")
                    }else{
                        console.log("Not matched!")
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
        text-decoration: line-through;
    }
</style>