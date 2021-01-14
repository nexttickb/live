<template>
	<div class="left-menus">
		<ul>
			<li v-for="(value, key) in onlineData.onlineList" class="slideOutUp" :class="{active: value.active}" @click="onMenuClick(key, value)"><a>id:{{value.name}}</a></li>
		</ul>
	</div>
</template>

<script>
export default {
  name: 'onlineList',
  data () {
    return {
    	msg: 'Dad Says:',
		onlineData:{
			onlineList:{
				"1111111":{name:"hello0", active:0},
				"1111112":{name:"hello1", active:1},
				"1111113":{name:"hello2", active:0},
				"1111114":{name:"hello3", active:0}
			}
		}
    }
  },
  props:['dadsay'],
  methods:{
	doSayHello:function(){
		this.$emit("testmsg", {id: "666", body:"hello"});	
	},
	onMenuClick:function(key, value){
		
	},
	addClient:function(id, info){
	
	},
	delClient:function(id){

	},
	getClient:function(id){
		
	}
  }
}
</script>

<style lang="less" scoped>
	@import '../assets/global.less';
	.left-menus{
		@left-menu-bg-color:#fff;
		@left-menu-active-color:#38f;
		@left-menu-height:35px;
		@left-menu-font-color:#666;
		color:@global-font-color;
		ul{
			margin:0px;
			padding:0px;
			li{
				list-style:none;
				cursor:pointer;
				width:@global-sidebar-width;
				height:@left-menu-height;
				margin-top:2px;
				text-align:center;
				background:@left-menu-bg-color;
				line-height:@left-menu-height;
				color:@left-menu-font-color;
			}
			.active{
				color:@left-menu-bg-color;
				background:@left-menu-active-color;
			}
		}
	}
</style>
