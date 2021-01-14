<template>
	<div class="tab-control">
		<div v-for="item in tabItem" class="tab" :class="{active:item.show}" @click="active(item.id)">
			<span class="title">{{item.title}}</span>
			<span @click="close(item.id)" class="close" :class="{hide:item.closeBtn}">×</span>
		</div>
	</div>
</template>

<script>
export default {
  name: 'tabControl',
  data () {
    return {
    	msg: 'Dad Says:',
		cbfunc:null,
		tabItem:[],
		tabIndex:0,
		mPreIndex:[]
    }
  },
  props:['dadsay'],
  mounted:function(){
		this.addTab({'title':'baidu1', "url":"http://www.sinbt.com", "id":1, "btnClose":false});	
  },
  methods:{
	doSayHello:function(){
		this.$emit("testmsg", {id: "666", body:"hello"});	
	},
	'addTab':function(tabItem){
			//var id = this.tabIndex++;
			if(this.getIndexById(tabItem.id) >= 0)
			{
				return this.active(tabItem.id);
			}
			this.mPreIndex.push(tabItem.id);
			if(typeof(tabItem.url) == "undefined")
			{
				this.tabItem.unshift({title:tabItem.title, url:"", el:tabItem.el, func:tabItem.func, id:tabItem.id, show:false, closeBtn:tabItem.closeBtn});
			}else{
				this.tabItem.unshift({title:tabItem.title, url:tabItem.url, id:tabItem.id, show:false, closeBtn:tabItem.closeBtn});
			}
			this.active(tabItem.id);
		},
		'reload':function(id){
			try{
				document.frames("iframe_" + id).location.reload();
			}catch(e){
			}
		},
		'showPanel':function(id, bl){
			var item = this.tabItem[this.getIndexById(id)];
			if(typeof(item.el) != "undefined")
			{
				var obj = document.getElementById(item.el);
				if(obj != null)
				{
					obj.style.display = (bl?"block":"none");
				}
				if(bl)
				{
					item.func.call(0, id);
				}
			}
		},
		'getIndexById':function(id){
			for(var i = 0; i < this.tabItem.length; i++)
			{
				if(this.tabItem[i].id == id)
				{
					return i;
				}
			}
			return -1;
		},
		'close':function(id){
			this.clearIndex(id);
			this.autoActive();
			this.tabItem.splice(this.getIndexById(id), 1);
			this.showPanel(id, 0);
		},
		'active':function(id){
			if(this.mPreIndex[this.mPreIndex.length - 1] != id)
			{
				this.mPreIndex.push(id);
				if(this.mPreIndex.length > 99)
				{
					this.mPreIndex.splice(0, 1);
				}
			}
			if(this.mPreIndex.length > 0){
				var preId = this.mPreIndex[this.mPreIndex.length - 2];
				var index = this.getIndexById(preId);
				if(typeof(this.tabItem[index]) != "undefined")
				{
					this.tabItem[index].show = false;
					this.showPanel(preId, 0);
				}
			}
			this.tabItem[this.getIndexById(id)].show = true;
			this.showPanel(id, 1);
		},
		'clearIndex':function(id){
			for(var i = 0; i < this.mPreIndex.length; i++)
			{
				if(this.mPreIndex[i] == id)
				{
					this.mPreIndex.splice(i, 1);
					this.clearIndex(id);
					this.showPanel(id, 0);
				}
			}
		},
		'autoActive':function(){
			this.active(this.mPreIndex[this.mPreIndex.length - 1]);
		}
  }
}
</script>

<style lang="less" scoped>
	@import '../assets/global.less';
	.tab-control{
		height:@global-right-top-height - @global-ly-right-top-botton;
		background-color:@global-background-color;
		border-bottom:@global-ly-right-top-botton solid @global-tab-bg-color;
			.tab{
				height:@global-tab-height - @global-ly-right-top-botton;
				padding-left:@global-box-margin;
				padding-right:@global-box-margin;
				line-height:@global-tab-height;
				background-color:@global-tab-bg-color2;
				float:left;
				margin-left:@global-box-margin;
				width:@global-tab-item-width;
				color:@global-tab-bg-color/2;
				cursor:default;
				.title{
					width:@global-tab-item-width - 60px;
					text-overflow:ellipsis;
					white-space:nowrap;
				}
				.close{
					cursor:pointer;
					float:right;
				}
			}
			.active{
				background-color:@global-tab-bg-color;
				color:@global-tab-bg-color * 5;
			}
	}
</style>
