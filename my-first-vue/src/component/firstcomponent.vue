<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<h1>{{ myfatherhello }}</h1>
		<button v-on:click="onClickMe">open mouse!</button>
	</div>
</template>

<script>
	export default{
		data: function(){
			return {
				msg: 'hello from component a!'
			}
		},
		props: ['myfatherhello'],
		methods: {
			onClickMe: function(){
				//  console.log(this.myfatherhello)
				this.$emit('child-tell-me-something',this.msg)
			}
		}
	}
</script>

<style>
	h1{
		color:#42B983;
	}
	
</style>