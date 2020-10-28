<template>
  <div id="app">
    <Nav/>
    <HelloWorld/>
    <Calc />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Calc from './components/calc.vue'
import Nav from './components/nav.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    Calc,
    Nav
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
}
body {
	background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
	background-size: 1000% 1000%;
	animation: gradient 15s ease infinite;
}

@keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}
</style>
