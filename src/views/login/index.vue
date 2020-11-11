<template>
  <div class="login-container">
    <div class="left-box">
      <div class="title-box">
        <img src="@/assets/login-logo.png" alt="" />
        <span class="title">黑马面面</span>
        <span class="line"></span>
        <span class="sub-title">用户登录</span>
      </div>
      <el-form ref="form" :model="form" :rules="rules">
        <el-form-item prop="phone">
          <el-input
            placeholder="请输入手机号"
            prefix-icon="el-icon-user"
            v-model="form.phone"
          >
          </el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            placeholder="请输入密码"
            prefix-icon="el-icon-lock"
            v-model="form.password"
            show-password
          >
          </el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-col :span="16">
            <el-input
              placeholder="请输入验证码"
              prefix-icon="el-icon-key"
              v-model="form.code"
            >
            </el-input>
          </el-col>
          <el-col :span="8">
            <img src="http://127.0.0.1/heimamm/public/captcha?type=login" alt="" class="code" />
          </el-col>
        </el-form-item>
        <el-form-item prop="checked">
          <el-checkbox v-model="form.checked"
            >我已阅读并同意 <el-link type="primary">用户协议</el-link>和
            <el-link type="primary">隐私条款</el-link>
          </el-checkbox>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="primary" @click="register">注册</el-button>
        </el-form-item>
      </el-form>
    </div>
    <img src="@/assets/login_banner_ele.png" alt="" />
  </div>
</template>

<script>
import { userLogin } from '@/api/login.js'
export default {
  name: "login",
  data() {
    return {
      form: {
        phone: "",
        password: "",
        code: "",
        checked: [],
      },
      rules: {
        phone: [
          { required: true, message: "请输入手机号", trigger: "blur" },
          { pattern:/^(0|86|17951)?(13[0-9]|15[012356789]|166|17[3678]|18[0-9]|14[57])[0-9]{8}$/, message: "手机号格式错误", trigger: "change" },
        ],
        password: [
          { required: true, message: "请输入密码", trigger: "blur" },
          { min: 6, max: 12, message: "长度在 6 到 12 个字符", trigger: "change" },
        ],
        code: [
          { required: true, message: "请输入验证码", trigger: "blur" },
          { min: 4, max: 4, message: "验证码长度4个字符", trigger: "change" },
        ],
        checked: [
          { required: true, message: "必须要同意", trigger: "change" },
        ],
      },
    };
  },
  methods: {
    login(){
       this.$refs.form.validate((valid) => {
          if (valid) {
            userLogin({
              phone:this.form.phone,
              password:this.form.password,
              code:this.form.code,
            }).then(res=>{
              //成功回调
              console.log(res);
            });
          } else {
            // console.log('error submit!!');
            this.$message.error('数据格式有误');
            return false;
          }
        });
    },
    onSubmit() {
      console.log("submit!");
    },
  },
};
</script>

<style lang="less">
.login-container {
  height: 100%;
  background: linear-gradient(#1493fa 28%, #01c6fa 96%);
  display: flex;
  align-items: center;
  justify-content: space-around;
  .left-box {
    width: 478px;
    height: 550px;
    background: #f5f5f5;
    padding: 44px;
    .title-box {
      display: flex;
      align-items: center;
      margin-bottom: 31px;
      img {
        margin-left: 48px;
        margin-right: 13px;
        width: 25px;
        height: 18px;
      }
      span {
        &.title {
          font-size: 24px;
          color: #0c0c0c;
        }
        &.line {
          width: 1px;
          height: 28px;
          background: #c7c7c7;
          margin-left: 14px;
          margin-right: 12px;
        }
        &.sub-title {
          font-size: 22px;
          color: #0c0c0c;
        }
      }
    }
    .code {
      width: 100%;
      height: 40px;
    }
    .el-checkbox {
      display: flex;
      align-items: center;
      .el-checkbox__input {
        transform: translateY(2px);
      }
      .el-checkbox__label {
        display: flex;
        align-items: center;
      }
    }
    .el-button {
      width: 100%;
      margin-left: 0;
      margin-top: 26px;
    }
  }
}
</style>
