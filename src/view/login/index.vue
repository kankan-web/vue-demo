<template>
  <div class="login-container">
    <el-form
      class="login-form"
      ref="loginFromRef"
      :model="loginForm"
      :rules="loginRules"
    >
      <div class="title-container">
        <h3 class="title">用户登录</h3>
      </div>
      <el-form-item prop="username">
        <span class="svg-container">
          <svg-icon icon="user" />
        </span>
        <el-input
          aria-placeholder="username"
          name="username"
          type="text"
          v-model="loginForm.username"
        >
        </el-input>
      </el-form-item>
      <el-form-item>
        <span class="svg-container">
          <svg-icon icon="password" />
        </span>
        <el-input
          placeholder="password"
          name="password"
          :type="passwordType"
          v-model="loginForm.password"
        >
        </el-input>
        <span class="show-pwd">
          <svg-icon
            :icon="passwordType === 'password' ? 'eye' : 'eye-open'"
            @click="onChangePwdType"
          />
        </span>
      </el-form-item>
      <el-button
        type="primary"
        style="width: 100%; margin-bottom: 30px"
        :loading="loading"
        @click="handleLogin(loginFromRef)"
        >登录</el-button
      >
    </el-form>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";
// import { useRouter } from "vue-router";
import { validatePassword } from "./rules";
import type { ElForm, FormInstance } from "element-plus";

//数据源
const loginForm = ref({
  username: "super-admin",
  password: "123456",
});
//验证规则
const loginRules = ref({
  username: [
    {
      required: true,
      trigger: "blur",
      message: "用户名不能为空",
    },
  ],
  password: [
    {
      required: true,
      trigger: "blur",
      validator: validatePassword(),
    },
  ],
});

// 处理密码框文本显示状态
const passwordType = ref("password");
const onChangePwdType = () => {
  if (passwordType.value === "password") {
    passwordType.value = "text";
  } else {
    passwordType.value = "password";
  }
};

//登录动作处理
const loading = ref(false);
const loginFromRef = ref<FormInstance>();
// const store = useStore()
// const router = useRouter();
const handleLogin = (formEl: FormInstance | undefined) => {
  if (!formEl) return;
  formEl.validate(async (valid) => {
    if (!valid) return;
    loading.value = true;
    try {
      //1.执行登录操作
      
    } catch (err) {
      console.error(err);
    } finally {
      loading.value = false;
    }
  });
};
</script>
<style lang="scss" scoped>
$bg: #2d3a4b;
$dark_gray: #889aa4;
$light_gray: #eee;
$cursor: #fff;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;
  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 160px 35px 0;
    margin: 0 auto;
    overflow: hidden;
    // 标题部分
    .title-container {
      position: relative;
      .title {
        font-size: 26px;
        color: $light_gray;
        margin: 0px auto 40px auto;
        text-align: center;
        font-weight: bold;
      }
    }
    // 图标部分
    .svg-container {
      padding: 6px 5px 6px 15px;
      color: $dark_gray;
      vertical-align: middle;
      display: inline-block;
    }
    // 输入框部分
    :deep(.el-form-item) {
      border: 1px solid rgba(255, 255, 255, 0.1);
      background: rgba(0, 0, 0, 0.1);
      border-radius: 5px;
      color: #454545;
    }
    :deep(.el-input) {
      display: inline-block;
      height: 47px;
      width: 85%;
      .el-input__wrapper {
        width: 100%;
        background-color: transparent;
        box-shadow: none; //最新
        -webkit-appearance: none;
        border-radius: 0px;
        padding: 12px 5px 12px 15px;
        height: 47px;
      }
      .el-input__inner {
        color: $light_gray;
        caret-color: $cursor;
      }
    }
  }
}
</style>
