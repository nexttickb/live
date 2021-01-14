<template>
	<div class="min-bar-box">
		<span class="btn-min" @global-click="btnMin"></span>
		<span class="btn-max" @global-click="btnMax"></span>
		<span class="btn-close" @global-click="btnClose"></span>
	</div>
</template>

<script>
export default {
  name: 'minBarBox',
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
	/*==minbtn开始*/
    .min-bar-box {
        right:10px;
        height:@global-top-height;
        .btn-min,.btn-max,.btn-close {
            float:left;
            margin-left:5px;
            margin-right:5px;
            margin-top:(@global-top-height - @global-min-box-size)/2;
            width:@global-min-box-size;
            height:@global-min-box-size;
//          background: url(./img/topbar.png) no-repeat;
			background:#fff;
        }
        .btn-min{
            background-position: -18px -117px;
            &:hover{
                background-position: -18px -144px;
            }
        }
        .btn-max{
            background-position: -41px -117px;
            &:hover{
                background-position: -41px -144px;
            }
        }
        .btn-close{
            background-position: -86px -117px;
            &:hover {
                background-position: -86px -144px;
            }
        }
    }

/*==minbtn结束*/

</style>
