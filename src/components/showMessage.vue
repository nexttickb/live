<template>
	<div class="ly panel-show" v-el:messagelist>
		<button>查看历史消息</button>
		<div class="sin_content"> 

     		<div class="sin_conversation_item" v-for="item in message">
      			<div :class="{'sin_conv_innerwrap_left':item.type, 'sin_conv_innerwrap_right':!item.type}" > 
       				<div :class="{'sin_conv_left':item.type, 'sin_conv_right':!item.type}">{{item.text}}</div>
				</div>
			</div> 

    	</div>
	</div>
</template>

<script>
export default {
  name: 'showMessage',
  data () {
    return {
		message: [],
    	msg: 'Dad Says:'
    }
  },
  props:['dadsay'],
  mounted:function(){
	  this.addMessage(1, "asxaxs", "你好，这是一条测试消息!!!!!!!!!!!!!!!!!!!!!");
	  this.addMessage(0, "asxaxs", "你好，这还是一条测试消息.................................");
	  this.addMessage(0, "asxaxs", "你好，这还是一条测试消息.................................");
  },
  methods:{
	doSayHello:function(){
		this.$emit("testmsg", {id: "666", body:"hello"});	
	},
	addMessage:function(type, name, message){
		var _self = this;
		this.message.push({text: message, time:new Date().getTime(), name:name, type: type});
		setTimeout(function(){
			_self.$els.messagelist.scrollTop = _self.$els.messagelist.scrollHeight;
		}, 0);
	}
  }
}
</script>

<style lang="less" scoped>
	@import '../assets/global.less';
	.panel-show{
		top: @global-box-margin;
		left:@global-box-margin;
		right:@global-box-margin;
		bottom: @global-box-margin;
		background:#fff;
		overflow-y:scroll;
		.sin_conversation_item{margin:0;padding:8px 10px;width:auto}
		.sin_conversation_item a{text-decoration:none}
		.sin_conversation_item a div{text-decoration:none}
		.sin_conv_innerwrap_left{padding:0 8px;/*background:url(./arrow1.png) no-repeat left bottom;*/background-size:8px 25px}
		.sin_conv_innerwrap_right{overflow:hidden;padding:0 8px;/*background:url(./arrow2.png) no-repeat right bottom;*/background-size:8px 25px}
		.sin_conv_left,.sin_conv_right{padding:8px 12px;-webkit-border-radius:8px;-khtml-border-radius:8px;-moz-border-radius:8px;border-radius:8px;color:#333;font-size:16px;line-height:26px}
		.sin_conv_left{margin-right:auto;margin-left:0;max-width:50%;background-color:#eee}
		.sin_conv_right{float:right;display:inline;margin-right:0;margin-left:auto;max-width:50%;background-color:#00acec;color:#fff;text-align:right;word-break:break-all}
	}
</style>
