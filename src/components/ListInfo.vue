<template>
  <div>
    <div class="totle">
    		<div class="bookleft">
	    		<h1 class="title">{{data.title}}</h1>
	    		<div class="bookcon">
	    			<p><span class="pingjia">评价</span>{{data.rating_cnt}}人评价</p>
		    		<p>{{data.original_author}}</p>
		    		<p>{{data.kind}}</p>
		    		<p>{{data.publisher}}/{{data.publish_time}}</p>
		    		<p>{{data.round_word_count}}</p>
	    		</div>
    		</div>
    		<div class="bookright">
    				<img :src="data.cover" alt="" />
    		</div>
    </div>
    <div class="bookread">
    	<div class="readbutton">
    			<i class="iconfont icon-book"></i>
    			<span class="read">阅读</span>
    	</div>
    	<div class="fenxiang">
    			<i class="iconfont icon-fenxiang" @click="click">
    				<mt-actionsheet
						  :actions="actions"
						  :closeOnClickModal=false
						  v-model="flag">
						</mt-actionsheet>
    			</i>
    	</div>
    </div>
    <ul class="price">
    	<li class="priceleft">
    		￥{{data.fixed_price/100}}
    	</li>
    	<li class="buy">
    		<i class="iconfont icon-64d"></i>
    		购买
    	</li>
    	<li class="song">
    		<i class="iconfont icon-iconfontliwu"></i>
    		赠送
    	</li>
    </ul>
    <InfoSummary :jianjie="jianjie" :mvlu="mvlu" :tags="tags" :pinglun-id='id'></InfoSummary>
  </div>
</template>

<script>
	import Vue from 'vue'
	import InfoSummary from './InfoSummary'
	export default {
	  name: 'ListInfo',
	  components:{
			InfoSummary
	},
  data () {
    return {
    	arr:"",
    	data:"",
    	jianjie:"",
    	mvlu:"",
    	tags:"",
    	id:0,
    	actions:[{name:"分享至"},{name:"爱阅读"},{name:"新浪微博"},{name:"朋友圈"}],
    	flag:false
    }
  },
  methods:{
  			click:function(){
					 if(this.flag==true){
							this.flag=false;
						}else{
							this.flag=true;
						}
				}
  },
  created(){
  	//详情 https://read.douban.com/j/ebook/
  	//console.log(window.location);
  	this.id = window.location.pathname.split("/")[2];
  	//console.log(id);
  	var url = "https://read.douban.com/j/ebook/"+ this.id;
  	//console.log(url);

	   Vue.axios.get(url).then((res)=> {
        return res.data;
        console.log(res);
    }).then((data)=>{
      	this.data = data;
      	console.log(data);
      	this.jianjie = data.abstract;
      	this.mvlu = data.table_of_contents;
      	this.tags = data.tags;
	    })
	  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p{
	font-size:0.25rem;
	line-height:1.3;
	color:#a6a6a6;
	margin-bottom: 5px;
}
.totle{
	width:100vw;
	height:3.5rem;
	padding:0.35rem 0.3rem 0;
	background: white;
	border-top: 1px solid gainsboro;
}
.title{
	font-size: 0.3rem!important;
	font-weight: 900;
}
.bookcon{
	margin-top:0.2rem;
}
.bookleft{
	float: left;
	left:0.3rem;
	width: 70%;
}
.bookright{
	float: right;
	right:0.2rem;
	top:0.5rem;
	width: 30%;
}
.bookright img{
	width:1.9rem;
	height:2.58rem;
}
.bookread{
	height:0.8rem;
	background:white;
	padding:0 0.3rem 0;
}
.readbutton{
	float:left;
	height:0.6rem;
	width:4.8rem;
	background:#71ceb5;
	border-radius: 0.35rem;
	font-size: 0.3rem;
	color:white;
	text-align: center;
	line-height:0.6rem;
}
.fenxiang{
	float:right;
	width:0.6rem;
	height:0.6rem;
	color:#77a4b3;
	font-size: 0.3rem;
	border-radius: 0.3rem;
	text-align: center;
	line-height:0.6rem;
	border:1px solid #77a4b3;
}
.price{
	height:1rem;
	border:1px solid gainsboro;
	background: white;
}
.price li{
	float:left;
	font-size: 0.25rem;
}
.priceleft{
	width:60vw;
	height:1rem;
	line-height: 1rem;
	padding-left:0.4rem;
	font-size: 0.25rem;
}
.buy,.song{
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	width:19.5vw;
	height:1rem;
}
.buy{
	border-right: 1px solid gainsboro;
	border-left: 1px solid gainsboro;
}
.pingjia{
		font-size: .16rem;
		color: #fff;
		background: #71ceb5;
		border-radius: 2px;
		padding: 4px 12px;
		margin-right: 4px;
	}
</style>
