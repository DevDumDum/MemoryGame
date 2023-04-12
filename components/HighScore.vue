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
                      <h3>Steps : Pairs</h3>
                    </div>
                    <div class="col-4">
                      <h3>Time</h3>
                    </div>
                </div>
                <div style="width:100%; height: 100%; overflow-y: scroll; max-height: 350px;">
                  <div class="row" v-for="score in scores" :key="score.id">
                      <div class="col-4">
                        <h1>{{ score.name }}</h1>
                      </div>
                      <div class="col-4">
                        <h1>{{ score.steps }}&nbsp;&nbsp;:&nbsp;&nbsp;{{ score.pairs }}</h1>
                      </div>
                      <div class="col-4">
                        <h1>{{ score.time }}</h1>
                      </div>
                  </div>
              </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ["hs"],
  data() {
    return {
      scores: this.hs,
    };
  },
  mounted(){
    console.log(this.hs);
  }
};
</script>