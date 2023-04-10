<template>
    <div id="mWrapper">
        <div id="MainMenu">
            <img @click="$emit('pageS',0)" id="closeBtn" src="../assets/web/playisclicked/close.png">
            <div id="mContainer">
                <div id="difficulty">
                    <div v-if="!gameStarted" id="btnWrapper">
                        <img class="btn" src="../assets/web/playisclicked/EASY.png" @click="setDifficulty(2, 4)"><br>
                        <img class="btn" src="../assets/web/playisclicked/HARD.png" @click="$emit('pageS',1)"><br>
                        <img class="btn" src="../assets/web/playisclicked/MEDIUM.png" @click="$emit('pageS',1)"><br>
                        <img class="btn" src="../assets/web/HOME/PLAY.png" @click="$emit('user-name','')">
                    </div>
                      <div v-else class="pausewindow">
                            <Card :items="shuffleItems"/>
                            
                        <br><button class="pausebutton" @click="showModal = true">Pause Game</button>
                    <div v-if="showModal" class="modal">
                        <div class="modal-content">
                                <!-- <h2>Game Paused</h2> -->
                                <!-- <img class="pause" src="../assets/web/paused/BG.png" @click="showModal = true"><br> -->
                                <!-- <img src="../assets/web/paused/BG.png" alt=""> -->
                                <div class="modal-image"> 
                                    <div class="resume">
                                         <img src="../assets/web/paused/PAUSE.png">
                                    </div>
                                    <p><i>The game is paused. Click back button to resume. Click close button to exit</i></p>
                            <div class="modal-buttons">
                                <img class="back" src="../assets/web/paused/BACK.png" @click="showModal = false"><br>
                                <img class="back" @click="$emit('pageS',0)" src="../assets/web/playisclicked/close.png">
                                <!-- <button class="no" @click="showModal = false">No</button>
                                <button class="yes" @click="resumeGame()">Yes</button> -->
                            </div>
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
                size: null,
                showModal: false,
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
            resumeGame() {
            // Code to resume the game
            this.showModal = false;
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