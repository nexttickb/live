<template>
  <div class="hello">
    <h1>{{ msg }}{{dadsay}}</h1>
	<button @click="doSayHello">say hello</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Dad Says:'
    }
  },
  props:['dadsay'],
  methods:{
	doSayHello:function(){
		this.$emit("testmsg", {id: "666", body:"hello"});	
	}  
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
