<template>
  <div class="login">
    <el-card class="card">
      <div class="logo">
        <img src="../../assets/imgs/logo_index.png" alt="">
      </div>
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" style="margin-top:20px">
        <el-form-item prop="mobile">
          <el-input v-model="ruleForm.mobile"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input v-model="ruleForm.code" style='width:250px'></el-input>
          <el-button style='float:right'>发送验证码</el-button>
        </el-form-item>
        <el-form-item prop="check">
          <el-checkbox v-model="ruleForm.check">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button @click="login" style='width:100%' type="primary">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    let validator = function (rule, value, callBack) {
      if (value) {
        callBack()
      } else {
        callBack(new Error('请勾选'))
      }
    }
    return {
      ruleForm: {
        mobile: '',
        code: '',
        check: false
      },
      rules: {
        mobile: [{
          required: true,
          message: '请输入手机号'
        }, {
          pattern: /^1[3456789]\d{9}$/,
          message: '手机号格式不正确'
        }],
        code: [{
          required: true,
          message: '请输入验证码'
        }, {
          pattern: /^\d{6}$/,
          message: '验证码格式不正确'
        }],
        check: [{
          validator
        }]
      }
    }
  },

  methods: {
    login () {
      this.$refs.ruleForm.validate(isok => {
        if (isok) {
          this.$message({ type: 'success', message: '登陆成功' })
        } else {
          this.$message({ type: 'warning', message: '登录失败' })
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
  .login {
    background-image: url('../../assets/imgs/login_bg.jpg');
    background-size: cover;
    height:100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    .card {
      width: 440px;
      height: 350px;
      .logo {
        text-align: center;
        img {
          height: 45px;
        }
      }
    }
  }
</style>
