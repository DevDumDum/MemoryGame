<script>
import MemoryGame from '../components/MemoryGame.vue'
// import HighScore from '../components/HighScore.vue'
// import LevelComplete from '@/components/LevelComplete.vue'

export default {
  name: 'IndexPage',
  components: {
    MemoryGame,
    // HighScore,
    // LevelComplete
  },
  // data() {
  //   return {
  //     currentLevel: 1,
  //     levelComplete: false
  //   }
  // },
  // methods: {
  //   advanceLevel() {
  //     this.currentLevel++
  //     this.levelComplete = false
  //   }
// }
}
</script>

<template>
  <body>
      <MemoryGame/>
  </body>
</template>
