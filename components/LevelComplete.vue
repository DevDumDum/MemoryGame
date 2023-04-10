<template>
    
    <div>
      <h2>Congratulations!</h2>
      <p>You have completed level {{ level }}!</p>
      <button @click="nextLevel">Next Level</button>
      <level-complete v-if="levelComplete" :level="currentLevel" @next-level="advanceLevel" />
    </div>
  </template>
  
  <script>
  export default {
    props: {
      level: {
        type: Number,
        required: true
      }
    },
    methods: {
      nextLevel() {
        this.$emit('next-level')
      }
    }
  }
  </script>