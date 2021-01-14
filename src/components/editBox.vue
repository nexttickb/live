<template>
	<div class="ly input" contenteditable="true" id="sendbufbox"></div>
</template>

<script>
export default {
  name: 'editBox',
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
	.input{
		padding:@global-box-margin;
		-webkit-box-shadow:0 0 5px #222 inset;
		top: @global-box-margin;
		left:@global-box-margin;
		right:@global-box-margin;
		bottom: @global-box-margin;
		outline:none;
		overflow-y:scroll;
		transform: translate(0,0);
		transition:all .2s ease-in 0s;
		&:focus{
			-webkit-box-shadow:0 0 15px #00f inset;
		}
	}
</style>
