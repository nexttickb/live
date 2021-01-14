<template>
	<div class="">
		<div class="ly message-panel">
			<div class="ly panel-top">
				<h3>hello</h3>	
			</div>
			<div class="ly panel-body">
				<show-message></show-message>
			</div>
			<div class="ly panel-bottom">
				<div class="ly panel-toolbar">
					<mini-toolbar></mini-toolbar>	
				</div>
				<div class="ly panel-input">
					<edit-box></edit-box>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import showMessage from './showMessage.vue'
import miniToolBar from './miniToolBar.vue'
import editBox from './editBox.vue'
export default {
  name: 'messageBox',
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
  },
  components:{
  	'show-message': showMessage,
  	'mini-toolbar': miniToolBar,
  	'edit-box': editBox 
  }
}
</script>

<style lang="less" scoped>
	@import '../assets/global.less';
	.message-panel{
		@head-height:45px;
		@bottom-height:130px;
		@toolbar-height:30px;
		top:0px;
		left:0px;
		right:0px;
		bottom:0px;
		.panel-top, .panel-body, .panel-bottom, .panel-toolbar, .panel-input{
			left:0px;
			right:0px;
			width:100%;
		}
		.panel-top{
			top:0px;
			height:@head-height;
			background: -webkit-linear-gradient(top, #fff, #eee, #dedede);
		}
		.panel-body{
			top:@head-height;
			bottom:@bottom-height;
			background:#ccc;
		}
		.panel-bottom{
			bottom:0px;
			height:@bottom-height;
			.panel-toolbar{
				height:@toolbar-height;
				top:0;
				background:#ff0;
			}
			.panel-input{
				top:@toolbar-height;
				height:@bottom-height - @toolbar-height;
			}
		}
		
	}
</style>
