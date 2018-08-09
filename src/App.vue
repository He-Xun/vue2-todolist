<template>
	<div id="app">
		<!--<img src="./assets/logo.png">-->
		<!--<HelloWorld/>-->
		<TodoList/>
	</div>
</template>

<script>
    import HelloWorld from './components/HelloWorld'
    import TodoList from './components/TodoList'

    export default {
        name: 'App',
        components: {
            // HelloWorld,
            TodoList
        }
    }
</script>

<style>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
