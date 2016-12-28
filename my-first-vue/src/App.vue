<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew"/>
    <ul>
    	  	<li v-for="item in items" 
    	  		v-bind:class="{finished: item.isFinished}"
    	  		v-on:click="toggleFinish(item)">
    	  		{{ item.label }} 
    	  	</li>
    </ul>
    <p>child tells me: {{ childWords }}</p>
   <firstcomponent myfatherhello="nihao"
   	v-on:child-tell-me-something="listenToMyBoy"></firstcomponent>
  </div>
</template>

<script>
import Store from './store'
import firstcomponent from './component/firstcomponent.vue'

export default {
  name: 'app',
  data : function () {
    return {
      title: 'this is a todo list',
      items: Store.fetch(),  
      newItem: '',
      childWords: ''   //必须在data里注册，并声明
    }
  },
  components: {firstcomponent},
  watch: {
  	items: {
  		handler: function(items){
  			Store.save(items)
  		},
  		deep: true    //监视状态的更新
  	}
  },
  methods: {
  	toggleFinish: function(item){
      	console.log(item.isFinished = !item.isFinished)
     },
     addNew: function(){
     	this.items.push({
     		label: this.newItem,
     		isFinished: false
     	})
     	this.newItem = ''
     },
     listenToMyBoy: function (msg){
     	this.childWords = msg
     }
  }
}
</script>

<style>
.finished{ 
	text-decoration: underline;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
