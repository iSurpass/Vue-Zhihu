<template>
  <div class="desktop">
    <Content1 v-for="item in zhihus" :key="item.about" :zhihu="item"></Content1>
    <div class="has-text-centered" v-show="loadMoring">
      正在加载...
    </div>
  </div>
    
  
</template>

<script>
import Content1 from "./inforList/components/content.vue";
import Vue from 'vue';

export default {
  name: "inforList",
  data: function() {
    let zhihus = [];
    for (let i = 0; i < 30; i++) {
      zhihus.push({
        about: "热门内容,来自:社交网络",
        icon:
          "https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=3797481993,1929347741&fm=27&gp=0.jpg",
        nickName: "秃头小白" + i,
        question: "为什么抖音里的帅哥美女那么多?",
        img:
          "https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=514630004,123217778&fm=26&gp=0.jpg",
        infor:
          "用" +
          i +
          "张图说明一切。前方高能！！！胆小者，心理承受能力差的就别往下看了。",
        stars: 12800 + 1000 * i,
        comments: 2403 + 2300 * i
      });
    }
    return {
      loadMoring:true,
      loading : false,
      zhihus:zhihus,
      page: {
        totalCount: 0,
        totalPage: 0,
        pageNum: 1,
        pageSize: 10,
        zhihus: []
      }
    };
  },
  mounted: function() {
    window.addEventListener("scroll",this.scrollFn)
    this.page.totalCount = this.zhihus.length;
    let countData = this.page.totalCount;
    let temp = countData % this.page.pageSize;
    let pageNum = parseInt(countData / this.page.pageSize);
    if (temp > 0) {
      pageNum++;
    } else if (temp < 0) {
      pageNum = 1;
    }
    this.page.totalPage = pageNum;
    this.getData();
  },
  methods: {
    scrollFn:function(){
      let pageHeight = Math.max(
        document.body.scrollHeight,
        document.body.offsetHeight
      );
      let viewHeight =
      window.innerHeight ||
      document.documentElement.clientHeight ||
      document.body.clientHeight ||
      0;
      let scrollHeight = 
      window.pageYOffset ||
      document.documentElement.scrollTop ||
      document.body.scrollTop ||
      0;
      let position = pageHeight - viewHeight - scrollHeight;
      if(position < 20){
        this.nextPageData();
      }
    },
    nextPageData:function(){
      if(this.page.pageNum===this.totalPage){
        this.loadMoreing =  false;
        return;
      }
      if(this.loading){
        return;
      }
      this.loading = true;
      this.page.pageNum++;
      let scrollHeight = document.body.scrollHeight;
      setTimeout(()=>{
          this.getData();
          this.loading = false;
          Vue.nextTick(function(){
            document.documentElement.scrollTop = scrollHeight;
          });
     },1000)
    },
    getData: function() {
      let start = (this.pageNum - 1) * this.page.pageSize;
      let end = start + this.page.pageSize;
      if (end > this.page.totalCount) {
        end = this.page.totalCount;
      }
      let curData = this.zhihus.slice(start,end);
      this.page.zhihus = this.page.zhihus.concat(curData);
    }
  },
  components: {
    Content1
  }
};
</script>

<style scoped>
.desktop {
  margin: 0;
  position:relative;
  width: 100%;
  height: 100%;
  top: 0;
  background-color: rgb(240, 240, 240);
}
</style>
