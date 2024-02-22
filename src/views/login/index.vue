<template>
  <div class="login-container">
    <div class="login-image"></div>
    <el-card class="login-card" shadow="always">
      <el-form class="login-form" ref="form" autocomplete="false" :model="loginForm" :rules="loginRules">
        <el-form-item>
          <h2>登录</h2>
        </el-form-item>
        <el-form-item prop="username">
          <el-input placeholder="请输入用户名" type="text" prefix-icon="el-icon-user" v-model="loginForm.username"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input placeholder="请输入密码" type="password" prefix-icon="el-icon-lock"
            v-model="loginForm.password"></el-input>
        </el-form-item>
        <el-form-item prop="isAgree">
          <el-checkbox v-model="loginForm.isAgree">我已阅读并同意《用户协议》</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" style="width: 100%" @click="login">登录</el-button>
        </el-form-item>
      </el-form></el-card>
  </div>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      // 登录表单的数据
      loginForm: {
        username: "",
        password: "",
        isAgree: "",
      },
      // 登录表单的验证
      loginRules: {
        username: [
          {
            required: "true",
            message: "请输入用户名",
            triger: "blur",
          },
        ],
        password: [
          {
            required: "true",
            message: "请输入密码",
            triger: "blur",
          },
          {
            min: "6",
            max: "16",
            message: "密码长度应位于6-16位之间",
          },
        ],
        isAgree: [{
          validator: (rule, value, callback) => {

            value ? callback() : callback(new Error('请阅读并勾选用户协议'))
          }
        }],
      },
    };
  },
  methods: {
    login() {
      this.$ref.form.validator((isOK) => {
        isOK ? alert(123) : ""
      })
    }
  }
};
</script>

<style lang="scss" scoped>
.login-container {
  height: 100vh;
  display: flex;
  background: linear-gradient(to bottom, #f8f9fa, #e9f2fe);

  .login-image {
    width: 60%;
    background-color: pink;
    border-radius: 0 200px 0 0;
    background-image: url("../../assets/bg/th (2).jpg");
    background-repeat: no-repeat;
    background-position: -200px 0;
    background-size: cover;
    background-attachment: fixed;
  }

  .login-card {
    width: 400px;
    margin: auto;
    background-color: #fff;
    border-radius: 20px;

    .login-form {
      padding: 0 10px;
    }
  }
}
</style>
