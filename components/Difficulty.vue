<template>
    <div id="mWrapper">
        <div id="MainMenu">
            <img @click="$emit('pageS',0)" id="closeBtn" src="../assets/web/playisclicked/close.png">
            <div id="mContainer">
                <div id="difficulty">
                    <div id="btnWrapper">
                        <img class="btn" src="../assets/web/playisclicked/EASY.png" @click="$emit('pageS',1)"><br>
                        <img class="btn" src="../assets/web/playisclicked/HARD.png" @click="$emit('pageS',1)"><br>
                        <img class="btn" src="../assets/web/playisclicked/MEDIUM.png" @click="$emit('pageS',1)"><br>
                        <img class="btn" src="../assets/web/HOME/PLAY.png" @click="$emit('user-name','')">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>