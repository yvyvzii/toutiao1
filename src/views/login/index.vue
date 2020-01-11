<template>
  <div class="login-container">

    <!-- 导航栏 -->
    <van-nav-bar  title="登录" />
    <!-- 导航栏 -->

    <!-- 表单 -->
    <van-cell-group>
      <van-field v-model="user.mobile" label="手机号" placeholder="请输入手机号" />

      <van-field v-model="user.code" label="验证码" placeholder="请输入验证码" >
        <van-count-down
        v-if="iscount"
          slot="button"
          :time="1000*60"
          format="mm 分 ss 秒"
          @finish="iscount=false"/>
       <van-button
          v-else
          slot="button"
          size="small"
          type="primary"
          round
          @click="onsendsms">
          发送验证码
        </van-button>
      </van-field>
    </van-cell-group>
    <!-- /表单 -->

    <!-- 登录按钮 -->
    <div class="login-btn-box login-btn-container">
      <van-button type="info" @click="onLogin" class="login-btn">登录</van-button>
    </div>
    <!-- /登录按钮 -->
  </div>
</template>

<script>
import { login, getsms } from '@/api/user'

export default {
  name: 'LoginPage',
  components: {},
  props: {},
  data () {
    return {
      user: {
        mobile: '',
        code: ''
      },
      iscount: false
    }
  },
  computed: {},
  watch: {},
  created () {},
  mounted () {},
  methods: {
    async onLogin () {
      const user = this.user
      this.$toast.loading({
        duration: 0, // 持续时间，0表示持续展示不停止
        forbidClick: true, // 是否禁止背景点击
        message: '登录中...' // 提示消息
      })

      try {
        const res = await login(user)
        console.log('登录成功', res)
        this.$toast.success('登录成功')
      } catch (err) {
        this.$toast.fail('登录失败，手机号或验证码错误')
      }
    },
    async onsendsms () {
      const { mobile } = this.user
      try {
        this.iscount = true
        await getsms(mobile)
      } catch (err) {
        console.log(err)
        this.iscount = false
        if (err.response.status === 429) {
          this.$toast('太过频繁的操作')
          return
        }
        this.$toast('发送失败')
      }
    }
  }
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
