<template>
        <div class="content">
            <div class="infor" style="margin:0px;padding:8px 8px 8px 8px">
                <div class="level is-mobile">
                    <div class="level-left">
                        <strong class="s1">{{zhihu.about}}</strong>
                    </div>
                </div>
                <div class="level is-mobile">
                    <div class="level-left">
                        <figure class="image is-32x32" style="margin:0px">
                            <img :src="zhihu.icon">
                        </figure>
                        <strong class="s2">{{zhihu.nickName}}</strong>
                    </div>
                </div>
                <div class="level is-moile">
                    <div class="level-left">
                        <strong class="s3">{{zhihu.question}}</strong>
                    </div>
                    <img :src="zhihu.img" class="img1">
                </div>
                <div class="level is-mobile">
                    <strong class="s4">
                        {{zhihu.infor}}
                    </strong>
                </div>
                <div class="level is-mobile">
                    <div class="level-left has-text-centered" style="color:rgb(81,128,186);background-color:rgb(230,240,250)">
                        <div class="level1">
                            <span class="icon is-big">
                                <i class="fas fa-caret-up"></i>
                            </span>
                            <strong style="font-size:15px;margin-left:5px;color:rgb(81,128,186);">赞同 {{formatStars}}</strong>
                        </div>

                    </div>
                    <div class="level-item has-text-centered" style="color:rgb(81,128,186);background-color:rgb(230,240,250);margin-bottom:5px">
                        <span class="icon is-small" style="width:30px;height:30px">
                            <i class="fas fa-caret-down"></i>
                        </span>
                    </div>
                    <div class="level-item">
                        <div class="level-item has-text-centered" style="color:rgb(130,130,150)">
                            <span class="icon is-small">
                                <i class="fas fa-comment"></i>
                            </span>
                            <strong style="margin-left:5px; color:rgb(130,130,150)">评论 {{formatComments}}</strong>
                        </div>
                        <div class="level-item has-text-centered" style="color:rgb(130,130,150)">
                            <span class="icon is-small">
                                <i class="fas fa-star"></i>
                            </span>
                        </div>
                        <div class="level-item has-text-centered" style="color:rgb(130,130,150)">
                            <span class="icon is-icon">
                                <i class="fas fa-ellipsis-h"></i>
                            </span>
                        </div>
                    </div>

                </div>
            </div>

        </div>
</template>

<script>
export default {
  name: "Content1",
  props:["zhihu",],
   computed: {
    formatStars: function() {
      if (this.zhihu.stars >= 1000) {
        return parseInt(this.zhihu.stars / 1000) + "K";
      } else {
        return this.zhihu.stars;
      }
    },
    formatComments: function() {
      if (this.zhihu.comments >= 1000) {
        var num = this.zhihu.comments / 1000;
        return num.toFixed(1)+ "K";
      } else {
        return this.zhihu.comments;
      }
    }
  },
};
</script>

<style scoped>
.level1 {
  margin: 3px 3px 3px 3px;
}
.level-item {
  margin: 5px 5px 5px 5px;
}
.level {
  margin: 6px;
}
.desktop {
  width: 100%;
  height: 667px;
  position: absolute;
  top: 0;
  background-color: rgb(240, 240, 240);
}
.content {
  margin: 7px;
  background-color: white;
}
.s1 {
  font-size: 17px;
  color: rgb(100, 100, 100);
}
.s2 {
  margin-left: 5px;
  font-size: 13px;
  color: black;
}
.s3 {
  font-size: 20px;
}
.s4 {
  font-size: 17px;
}
.img1 {
  height: 150px;
  width: 100%;
}
</style>

