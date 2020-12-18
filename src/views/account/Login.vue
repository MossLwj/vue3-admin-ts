<template>
  <div class="account">
    <div class="form-wrap">
      <a-form name="custom-validation" ref="ruleForm">
        <a-form-item name="username">
          <label>登录名</label>
          <a-input type="text" autocomplete="off" />
        </a-form-item>

        <a-form-item>
          <label>密码</label>
          <a-input type="password" autocomplete="off" />
        </a-form-item>

        <a-form-item>
          <a-button type="primary" html-type="submit" block>
            登录
          </a-button>
        </a-form-item>
      </a-form>
      <div class="text-center fs-12">
        <a href="" class="color-white">忘记密码</a>|
        <router-link to="/register">注册</router-link>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive } from "vue";
import { verifyPhone } from "@/utils/verification";
export default defineComponent({
  name: "Login",
  components: {},
  setup() {
    const checkUsername = async (rule: never, value: string): Promise<void> => {
      if (!value) {
        return Promise.reject("请输入用户名");
      }
      if (!verifyPhone(value)) {
        return Promise.reject("请输入11位手机号码");
      } else {
        return Promise.resolve();
      }
    };

    const formConfig = reactive({
      layout: {
        labelCol: { span: 4 },
        wrapperCol: { span: 14 }
      },
      rules: {
        username: [{ validator: checkUsername, trigger: "change" }]
      }
    });

    return {
      formConfig
    };
  }
});
</script>
<style lang="scss">
@import "./styles";
</style>
