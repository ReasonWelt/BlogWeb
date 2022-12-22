<!-- 友情链接模块 -->
<template>
<div class="tFriendsBox">
    <!-- 
        <h1>友链申请格式
        <h3>网站名称: XXXX</h3>
        <h3>网站地址: https://www.baidu.com </h3>
        <h3>网站描述: 百度你懂的</h3>
        <h3>网站logo: https://www.sg.com/1.png</h3>

     -->
    <h1>友情链接</h1>
    <el-row :gutter="10">
        <el-col :span="12" class="tf-item" v-for="(item,index) in friendslink" :key="'f'+index">
            <a :href="item.address" target="_blank">
                <img :src="item.logo?item.logo:'static/img/tou.jpg'"  :onerror="$store.state.errorImg">
                <h4>{{item.name}}</h4>
                <p>{{item.description}}</p>
            </a>
        </el-col>
    </el-row>


    <div class="rulbulink">
        <div >
            <img src="static/img/yangtao.jpg" style="max-width: 20%">
        </div>
        <!-- <span>
            <h1>友链申请</h1>
            <h3>网站名称: XXXX</h3>
            <h3>网站地址: https://www.baidu.com </h3>
            <h3>网站描述: 百度你懂的</h3>
            <h3>网站logo: https://www.sg.com/1.png</h3>
            <h3>【将上述信息发送到博主邮箱，验证安全后即可完成友链申请】</h3>
        </span> -->
    </div>

</div>
</template>

<script>
import {getAllLink} from '../api/link.js'
export default {
    data() { //选项 / 数据
        return {
            friendslink:[]//友情链接
        }
    },
    methods: { //事件处理器
        getList(){
            getAllLink().then((response)=>{
                this.friendslink = response
            })
        }
    },
    components: { //定义组件

    },
    created() { //生命周期函数
        this.getList()
    }
}
</script>

<style >
.tFriendsBox{
    background: #fff;
    padding:20px;
    border-radius: 5px;
    margin-bottom: 40px;
    transition: all 0.3s ease-out;
}
.tFriendsBox h1{
    padding:15px 0;
    font-size: 25px;
    font-weight: bold;
}
.tFriendsBox .tf-item{
    border-radius: 5px;
    position: relative;
    margin-bottom: 10px;
}
.tFriendsBox .tf-item a{
    display: block;
    border: solid 3px rgba(0, 0, 0, 0.1);
    padding:0 10px 0 90px;
    height:90px;
    transition: all 0.3s ease-out;
    border-radius: 5px;
}
.tFriendsBox .tf-item a:hover{
    /* background: #8fa6f17b; */
    border: solid 3px rgb(117, 152, 192);
    box-shadow: 0 15px 30px rgb(0 0 0 / 10%);
}
.tFriendsBox .tf-item a img{
    width:60px;
    height:60px;
    border-radius: 50%;
    position: absolute;
    top:15px;
    left:15px;
    cursor: pointer;
    object-fit: cover;
}
.tFriendsBox .tf-item a h4{
    cursor: pointer;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    font-size: 20px;
    padding-top:15px;
    font-weight: bold;
}
.tFriendsBox .tf-item a p{
    margin:10px 0;
    font-size: 12px;
    line-height: 24px;
    color:#999;
    cursor: pointer;
    white-space: nowrap;
    text-overflow: ellipsis;
}

.rulbulink{
    margin-top: 15px;
    padding: 15px;
    /* background-color: rgba(153, 153, 153, 0.162); */
    border-radius: 5px;
    text-align: right;
}

.rulbulink img{
    /* float: right; */
    margin-right: 0px;
}

.tFriendsBox:hover{
  transform: translate(0, -3px);
  box-shadow: 0 15px 30px rgb(0 0 0 / 10%);
}
</style>
