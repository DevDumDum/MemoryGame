# MemoryGame
![My Image](./assets/resource/1.png)

## Logged in user
displaying the Play, custom, Highscore, and Exit Button<br>
<img src="./assets/resource/2.png" width=49% height=50%> <img src="./assets/resource/3.png" width=49% height=50%>

## Custom Feature
User can input a number of custom pairs to play with by selecting the star icon on the menu. <img src="./assets/web/levelcomplete/STAR.png" width=5% height=5%><br><br>
<img src="./assets/resource/4.png" width=48%> <img src="./assets/resource/5.png" width=48%>

# Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev
```

## Directory
The working tree should look like this.<b4>
![My Image](./assets/resource/tree.png)

## Code for index.vue
Call the main component <MemoryGame />
```bash
<script>
import MemoryGame from '../components/MemoryGame.vue'

export default {
  name: 'IndexPage',
  components: {
    MemoryGame
  },
}
</script>

<template>
  <body>
      <MemoryGame/>
  </body>
</template>
```
