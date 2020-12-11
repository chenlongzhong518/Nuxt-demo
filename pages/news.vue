<template>
  <div class="container news-box">
    <div class="item title">新闻页</div>

    <div class="item">
      <div class="name">{{userInfo.name}}</div>
      <img :src="userInfo.avatar" alt class="avatar" />
    </div>

    <div class="item">
      <el-button type="primary" @click="getInfo()" :loading="loading">获取用户信息</el-button>
    </div>

    <div class="item">
      <nuxt-link to="/">
        <el-button type="primary">跳转</el-button>
     </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "news",
  components: {},
  data() {
    return {
      loading: false,
      userInfo: {
        name: "",
        avatar: ""
      }
    };
  },
  methods: {
    getInfo() {
      this.$store
        .dispatch("user/getInfo")
        .then(res => {
          this.userInfo = res;
          this.loading = false;
        })
        .catch(() => {
          this.loading = false;
        });
    }
  }
};
</script>
<style lang="scss">
.news-box {
  text-align: center;
  .item {
    text-align: center;
    margin-bottom: 20px;
    .title {
      color: #67c23a;
    }
    .avatar {
      width: px2rem(80);
      height: px2rem(80);
      display: block;
      margin: 0 auto;
      border-radius: 50%;
    }
  }
}
</style>
