<template>
  <div class="app">
	<div class="my-body">
		<div class="ly-top">
			<div class="ly img-y"></div>
			<div class="ly top-menus">
			</div>
			<div class="title-bar-min-box" style="float:right;">
				<min-bar-box></min-bar-box>
			</div>
		</div>
		<div><!--登录后显示的内容-->
			<div class="ly ly-left-top">
			</div>
			<div class="ly ly-left-body">
				<online-list></online-list>
			</div>
			<Message class="ly ly-right-body" style="background:#ccc;"></Message>
			<div class="ly ly-right-bottom">
				<div class="top"></div>
				<div class="bottom">
				</div>
			</div>
		</div>
	</div>
  </div>
</template>

<script>
import Hello from '@/components/Hello.vue'
import onlineList from '@/components/onlineList.vue'
import minBarBox from '@/components/minBarBox.vue'
import messageBox from '@/components/messageBox.vue'
import Message from '@/components/Message.vue'
import tabControl from '@/components/tabControl.vue'
export default {
	data() {
		return {
			userInfo:{
				token:"654321",
		  		userId:"u654321",
				name:"test1"
			},	
			serverInfo:{
				socket:{},
				serverAddr:"http://www.sinbt.com:8081/"	
			},
			isay:"i say hello"
		}
	},
	mounted:function(){
		this.init();	
	},
	methods: {
		init:function(){
			var self = this;
			this.connect2Server();
		},
		connect2Server:function(){
			var self = this;
			this.serverInfo.socket = io(this.serverInfo.serverAddr);
			this.socket.on('connect', function () {
				self.onConnected();	
			});
		},
		onConnected:function(){
			var self = this;
			this.socket.on('message', function (msg) {
				console.log(msg);
				self.onRecv(msg);	
			});
			this.doLogin();
		},
		doLogin:function(){
			this.sendData("login", {"name":name, uId:uId});
		},
		onLogin:function(data){
			this.userInfo.token = data.token;
			setInterval(function(){
				this.sendData("heart", {});
			}, 3000);
		},
		onMessage:function(data){
			console.log("recv message:", data);
		},
		onRecv:function(msg){
			switch(msg.type)
			{
				case "loginSuccess":
					this.onLogin(msg.body);
				break;
				case "message":
					this.onMessage(msg.body);
				break;
				case "userState":
					this.onUserState(msg.body);
				break;
				case "needLogin":
					this.doLogin();
				break;
			}
		},
		sendData:function(type, data){
			socket.send({type:type, token: this.userInfo.token, uId: this.userInfo.userId, body:data});
		},
		getMsgFromChld:function(msg){
			alert(msg.body);	
			console.log(this.$refs);
		}
	},
	components:{
		'hello': Hello,
		'min-bar-box': minBarBox,
		'online-list': onlineList,
		'message-box': messageBox,
		'Message':Message,
		'tab-control': tabControl 
	}
}
</script>

<style lang="less" scoped>
@import './assets/global.less';
@import './assets/app.less';
</style>
