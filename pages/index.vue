<template>
  <div class="container index-box">
    <div class="item title">首页</div>

    <div class="item">
      <img src="@/assets/images/logo.png" alt class="logo" />
    </div>

    <div class="item" v-if="!login_state">
      <el-button type="primary" @click="login()" :loading="loading">登录</el-button>
    </div>

    <div class="item" v-if="login_state">
      <nuxt-link to="/news">
        <el-button type="primary">跳转</el-button>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "index",
  components: {},
  data() {
    return {
      loading: false,
      loginForm: {
        username: "admin",
        password: "111111"
      },
      login_state: false
    };
  },
  methods: {
    login() {
      this.$store
        .dispatch("user/login", this.loginForm)
        .then(() => {
          this.$message({
            message: "登录成功",
            type: "success"
          });
          this.login_state = true;
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
.index-box {
  text-align: center;
  .item {
    text-align: center;
    margin-bottom: 20px;
    .title {
      color: #409eff;
    }
    .logo {
      width: px2rem(80);
      height: px2rem(80);
      display: block;
      margin: 0 auto;
    }
  }
}
</style>
