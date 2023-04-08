<script>
export default {
    props: ['pagestatus','userName'],
    emits: ['user-name'],
    data(){
        return{
            uname: ""
        }
    },
    created() {
        this.setViewport();
    },
    methods: {
        setUsername(x){
            if(x != ""){
                this.$emit('user-name', x);
                document.getElementById("uInput").value = "";
            }else{
                alert("Invalid user input");
            }
        },
        setViewport: function() {
            let changeWindowSize = 375
            let viewportContent = "width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"
            if (window.innerWidth < changeWindowSize ) {
                viewportContent = "width=375,user-scalable=no,viewport-fit=cover"
            }
            document.querySelector("meta[name='viewport']").setAttribute("content", viewportContent)
        }
        
    }
}
</script>

<template>
    <div id="mWrapper">
        <div id="MainMenu">
            <div id="mContainer">
                <div id="titleWrapper">
                    <div class="mTitleContainer">
                        <img class="mTitle" src="../assets/web/firstpage/MEMORY.png">
                    </div>
                    <div class="mTitleContainer">
                        <img class="mTitle2" src="../assets/web/firstpage/GAME.png">
                    </div>
                </div>

                <div v-if="(userName == '')" id="uInputWrapper">
                    <div id="uInputContainer">
                        <h2>Username:</h2><input id="uInput" v-model="uname" type="text" required/>
                    </div>
                    <div id="uInputButton">
                        <img src="../assets/web/firstpage/JOINBUTTON.png" id="join" @click="setUsername(uname)">
                    </div>
                </div>
                <div v-else>
                    <h1>Hi {{ userName }}!</h1><br>
                    <div style="display: flex; justify-content: center;">
                        <div id="btnWrapper">
                            <img class="btn" src="../assets/web/home/PLAY.png" @click="$emit('pageS',1)"><br>
                            <img class="btn" src="../assets/web/home/SCOREBOARD.png" @click="$emit('pageS',2)"><br>
                            <img class="btn" src="../assets/web/home/EXIT.png" @click="$emit('user-name','')">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>