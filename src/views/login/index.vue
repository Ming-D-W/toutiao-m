<template>
  <div class="login-container">
    <!-- 导航栏 -->
    <van-nav-bar class="page-nav-bar" title="登录"/>
    <!-- /导航栏 -->

    <!-- 登录表单 -->
    <van-form @submit="onSubmit">
      <van-field
        name="手机号"
        v-model="user.mobile"
        placeholder="请输入手机号"
      >
        <i slot="left-icon" class="toutiao toutiao-shouji"></i>
      </van-field>
      <van-field
        name="验证码"
        v-model="user.code"
        placeholder="请输入验证码"
      >
        <i slot="left-icon" class="toutiao toutiao-yanzhengma"></i>
        <template #button>
          <van-button class="send-sms-btn" round size="small" type="default">发送验证码</van-button>
        </template>
      </van-field>
      <div class="login-btn-wrap">
        <van-button class="login-btn" block type="info" native-type="submit">
          登录
        </van-button>
      </div>
    </van-form>
    <!-- /登录表单 -->
  </div>
</template>
<script>
import { login } from '@/api/user.js'
export default {
  name: 'LoginIndex',
  components: {},
  props: {},
  data () {
    return {
      user: {
        mobile: '',
        code: ''
      }
    }
  },
  computed: {},
  watch: {},
  created () {
  },
  mounted () {
  },
  methods: {
    // onSubmit (values) {
    //   console.log('submit', values)
    // }
    async onSubmit () {
      const user = this.user
      try {
        const res = await login(user)
        console.log('登录成功', res)
      } catch (err) {
        if (err.response.status === 400) {
          console.log('登录失败', err)
        }
      }
    }
  }
}
</script>
<style scoped lang="less">
.login-container {
  .toutiao {
    font-size: 24px;
  }

  .send-sms-btn {
    width: 90px;
    height: 26px;
    line-height: 46px;
    background-color: #ededed;
    font-size: 12px;
    color: #666;
  }

  .login-btn-wrap {
    padding: 53px 33px;

    .login-btn {
      background-color: #6db4fb;
      border: none;
      border-radius: 5px;
    }
  }
}
</style>
