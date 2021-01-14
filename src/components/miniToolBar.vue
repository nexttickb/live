<template>
	<div class="mini-tool-bar">
		<button>button</button>
	</div>
</template>

<script>
export default {
  name: 'miniToolBar',
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

<style lang="less" scoped>
	@import '../assets/global.less';
	.mini-tool-bar {
		
	}
</style>
