<!-- 搜索模块 -->
<template>
  <div class="tSearchBox tcommonBox">
    <header>
      <h1>
        <!-- <a href="#/DetailShare" target="_blank"> 搜索 </a> -->
        搜索
      </h1>
      <div class="search-box">
        <i class="fa fa-wa fa-search"></i>
        <el-input
          class="search-input"
          placeholder="请输入搜索关键字，将会从所有文章中筛选"
          v-model="searchData" 
          @change="getBackData()">
        </el-input>
      </div>
    </header>
    <section>
      <header>
        <el-row v-for="(item,index) in backData" :key="index" class="articleListBox searchList">
          <a :href="'#/DetailArticle?aid='+item.id">
           <div>
              <h1>
                {{index+1+". "}}{{item.title}}                    
              </h1>
              <h2>
                  <!-- <i class="fa fa-fw fa-user"></i>发表于 -->
                  <i class="fa fa-fw fa-clock-o"></i><span v-html="showInitDate(item.createTime,'all')">{{showInitDate(item.createTime,'all')}}</span> •
                  <i class="fa fa-fw fa-eye"></i>{{item.viewCount}} 次围观 •
              </h2>
              <p>
                  {{item.summary}}
              </p>
           </div>
          </a>
        </el-row>
      </header>
      <div>
        <img
          src="static/img/coffee.jpg"
          alt=""
          style="max-width: 20%"
          class="coffee"
        />
      </div>
      
      <hr />
      
    </section>
  </div>
</template>

<script>
import { initDate } from "../utils/server.js";
import { searchArticle } from "../api/article";

export default {
  data() {
    //选项 / 数据
    return {
      searchData: "",
      backData: []
    };
  },
  methods: {
    //事件处理器
    showInitDate: function(date, full) {
      //时间处理
      return initDate(date, full);
    },
    getBackData() {
      searchArticle(this.searchData).then(response => {
        this.backData = response;
      });
    }
  },
  components: {
    //定义组件
  },
  created() {
    //生命周期函数
    var that = this;
  },
  watch:{
    '$route'(){
      this.searchData = "";
      this.backData = [];
    }
  }
};
</script>

<style>

.searchList{
  border-bottom: solid 1px rgb(99, 198, 255);
  padding: 15px;
}


.tSearchBox section {
  padding-bottom: 20px;
}

.tSearchBox section h1 {
  margin: 10px 0;
  font-size: 20px;
  font-weight: 700;
  /*text-align: center;*/
  line-height: 30px;
}
.tSearchBox section p {
  margin: 10px 0;
  line-height: 10px;
  padding-left: 1.5em;
}
.tSearchBox section hr {
  background: #ccc;
  margin-bottom: 30px;
}

.tSearchBox .donate-item {
  text-align: right;
  color: #44b549;
}
.tSearchBox .donate-item:last-child {
  text-align: left;
  color: #00a0e9;
}
.tSearchBox .donate-item img {
  width: 100%;
  display: block;
  height: auto;
}
.tSearchBox .donate-item div {
  display: inline-block;
  width: 150px;
  padding: 0 6px;
  text-align: center;
  box-sizing: border-box;
}
.tSearchBox .donate-item div span {
  display: inline-block;
  width: 100%;
  margin: 10px 0;
  text-align: center;
}
.tSearchBox .el-table__body-wrapper {
  overflow: hidden;
}
.el-table--enable-row-hover .el-table__body tr:hover > td {
  background: transparent;
}

.search-box {
  padding: 10px;
  margin-top: 10px;
}

.search-box i {
  margin-left: 10px;
}

.search-input {
  width: 90%;
  margin: 5px 10px;
}
</style>
