<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>选项卡切换效果</title>


<style type="text/css">
*{
margin:0;
padding:0;
overflow:hidden;}
body{
font-family:微软雅黑}
.box{
width:270px;
margin:20px auto;}
.top{
height:26px;line-height: 26px;}
.title{display:inline-block;
font-size:22px;}
ul.tabs{display:inline-block;
list-style:none;
margin-left:70px;
}
ul.tabs li{
margin: 0;
padding: 0;
float:left;
width:50px;
height: 26px; 
line-height: 26px;
font-size:16px;
cursor:pointer;
text-align:center
}
ul.tabs li.active{
display:block;
width:50px;
height: 26px; 
line-height: 26px;
background-color:#66CCFF;
color:#FFFFFF;
cursor:pointer;}
.main{
clear:both;
margin-top:10px;}
.main div{
width:270px;
height:43px;
line-height:43px;
border-bottom-width: 1px;
border-bottom-style: dashed;
border-bottom-color: #333333;
background-color: #FFFFFF;
font-size:14px;}
.main div span{
margin-left:10px;
}
.main div span:last-child{
float:right;
margin-right:10px;
}
</style>
<script src="./vue.js"></script>
</head>
<body>
<div id="box">
	<div class="box">
		<div class="top">
			<span class="title">电影排行</span>
			<ul class="tabs">
				<li :class="{active : active}" v-on:mouseover="toggleAction('hit')">热播</li>
				<li :class="{active : !active}" v-on:mouseover="toggleAction('classic')">经典</li>
			</ul>
		</div>
		<component :is="current" :hitmovie="hitmovie" :classicmovie="classicmovie"></component>
	</div>
</div>
<script type="text/javascript">
//创建根实例
var vm = new Vue({
	el : '#box',
	data : {
		active : true,
		current : 'hit',
		hitmovie : [//热播电影数组
			{ name : '终结者5', star : '阿诺德.施瓦辛格' },
			{ name : '飓风营救', star : '连姆.尼森' },
			{ name : '我是传奇', star : '威尔.史密斯' },
			{ name : '一线声机', star : '杰森.斯坦森' },
			{ name : '罗马假日', star : '格里高利.派克' },
			{ name : '史密斯夫妇', star : '布拉德.皮特' },
			{ name : '午夜邂逅', star : '克里斯.埃文斯' }
		],
		classicmovie : [//经典电影数组
			{ name : '机械师2：复活', star : '杰森.斯坦森' },
			{ name : '变形金刚', star : '希亚.拉博夫' },
			{ name : '暮光之城', star : '克里斯汀.斯图尔特' },
			{ name : '怦然心动', star : '玛德琳.卡罗尔' },
			{ name : '电话情缘', star : '杰西.麦特卡尔菲' },
			{ name : '超凡蜘蛛侠', star : '安德鲁.加菲尔德' },
			{ name : '雷神', star : '克里斯.海姆斯沃斯' }
		]
	},
	methods : {
		toggleAction : function(value){
			this.current=value;
			value == 'hit' ? this.active = true : this.active = false;
		}
	},
	//注册局部组件
	components : {
		hit : {
			props : ['hitmovie'],//传递Prop
			template : `<div class="main"><div v-for="(item,index) in hitmovie">
    			<span>{{++index}}</span>
    			<span>{{item.name}}</span>
				<span>{{item.star}}</span>
  		  	  </div></div>`
		},
		classic : {
			props : ['classicmovie'],//传递Prop
			template : `<div class="main"><div v-for="(item,index) in classicmovie">
    			<span>{{++index}}</span>
    			<span>{{item.name}}</span>
				<span>{{item.star}}</span>
  		  	  </div></div>`
		}
	}
});
</script>













</body>
</html>
