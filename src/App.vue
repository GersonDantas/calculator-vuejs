<template>
  <div id="app">
    <h1>Calculator</h1>
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./main/Calculator"

export default {
    components: { Calculator }
}
</script>

<style>
@font-face {
  font-family: "RobotoThin";
  src: url("./fonts/Roboto-Thin.ttf");
}

* {
  font-family: "RobotoThin", "monospace";
}

body {
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
	color: #FFF;
}
</style>
