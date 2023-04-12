<script>
import MainMenu from './MainMenu.vue'
import Difficulty from './Difficulty.vue'
import HighScore from './HighScore.vue'

export default {
  components: {
    MainMenu,
    Difficulty,
    HighScore
  },
  data(){
    return{
      pageStatus: 0,
      username: '',
      highScore: []
    }
  },
  methods:{
    changePage(x){
      this.pageStatus = x;
    },

    setUserName(x){
      this.username = x;
    },
    setHighScore(x){
      this.highScore.push(x);
      console.log(this.highScore);
    }
  }
}
</script>

<template>
  <body>
    {{ pageStatus }}
      <main-menu v-if="pageStatus === 0" :pagestatus="pageStatus" @mainhighscore="setHighScore" :userName="username" @pageS="changePage" @user-name="setUserName"/>
      <!-- <Difficulty v-else-if="pageStatus === 1" @pageS="changePage" /> -->
      <HighScore v-else-if="pageStatus === 2" @pageS="changePage" :hs="highScore"/>
  </body>
</template>
