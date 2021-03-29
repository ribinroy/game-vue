<template>
  <div class="flex">
    <div class="main_wrap">
      <Game />
    </div>
  </div>
</template>

<script>
import Game from "./components/Game.vue";

export default {
  name: "App",
  components: {
    Game,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Bangers&display=swap");

body {
  font-family: "Bangers", cursive;
  margin: 0;
  background-color: #463788;
}
.flex {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}
.main_wrap {
  position: relative;
  width: 100%;
  height: 100%;
  max-width: 1920px;
  max-height: 1080px;
  background: url("assets/background Image.jpg");
}
</style>
