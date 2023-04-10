<template>
    <div id="mWrapper">
        <div id="MainMenu">
            <img @click="$emit('pageS',0)" id="closeBtn" src="../assets/web/playisclicked/close.png">
            <div id="mContainer">
                <h1>Highscore</h1>
                  <div class="row">
                      <div class="col-4">
                         <h3>Name</h3>
                      </div>
                      <div class="col-4">
                         <h3>Score</h3>
                       </div>
                      <div class="col-4">
                          <h3>Time</h3>
                       </div>
                       <ul>
                            <li v-for="score in scores" :key="score.id">
                                {{ score.playerName }} - {{ score.score }} : {{ score.time }}
                            </li>
                       </ul>
                      </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      scores: [
        { id: 1, playerName: 'John', score: 100 , time: '4 seconds'},
        { id: 2, playerName: 'Jane', score: 200 , time: '14 seconds'},
        { id: 3, playerName: 'Bob', score: 150 , time: '42 seconds'},
        { id: 4, playerName: 'Alice', score: 300 , time: '41 seconds'},
      ],
    };
  },
};
</script>