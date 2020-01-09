<template>
  <div class="login-container">

    <!-- 导航栏 -->
    <van-nav-bar title="登录" />
    <!-- 导航栏 -->

    <!-- 表单 -->
    <van-cell-group>
      <van-field label="手机号" placeholder="请输入手机号" />

      <van-field label="验证码" placeholder="请输入验证码" >
      <van-button slot="button" size="small" type="primary">发送验证码</van-button>
      </van-field>
    </van-cell-group>
    <!-- /表单 -->

    <!-- 登录按钮 -->
    <div class="login-btn-box">
      <van-button type="info">登录</van-button>
    </div>
    <!-- /登录按钮 -->
  </div>
</template>

<script>
export default {
  name: 'LoginPage',
  components: {},
  props: {},
  data () {
    return {}
  },
  computed: {},
  watch: {},
  created () {},
  methods: {}
}
</script>

<style scoped lang="less">
.login-container {
  .login-btn-container {
    padding: 20px;
    .login-btn {
      width: 100%;
    }
  }
}
</style>
