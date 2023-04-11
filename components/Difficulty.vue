<template>
    <div id="mWrapper">
        <div id="MainMenu">
            <span id="menuBtn">
                <img @click="$emit('pageS',0)" id="closeBtn" src="../assets/web/playisclicked/close.png">
            </span>
            <div id="mContainer">
                <div id="difficulty">
                    <div v-if="!gameStarted" id="btnWrapper">
                        <img class="btn" src="../assets/web/playisclicked/EASY.png" @click="setDifficulty(2, 4)"><br>
                        <img class="btn" src="../assets/web/playisclicked/HARD.png" @click="setDifficulty(2, 4)"><br>
                        <img class="btn" src="../assets/web/playisclicked/MEDIUM.png" @click="$emit('pageS',1)"><br>
                        <img class="btn" src="../assets/web/HOME/PLAY.png" @click="$emit('user-name','')">
                    </div>
                    <div v-else class="pausewindow">
                        <Card :items="shuffleItems"/>
                    </div>
                </div>
            </div>
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
                shuffleItems: [],
                size: null
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
            },
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