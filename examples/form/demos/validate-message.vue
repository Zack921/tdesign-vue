<template>
  <div>
    <!-- error-message 非必需 -->
    <t-form :data="formData" :rules="rules" ref="form" @reset="onReset" @submit="onSubmit" scrollToFirstError="smooth">
      <t-form-item label="用户名" help="这是用户名字段帮助说明" name="account">
        <t-input v-model="formData.account"></t-input>
      </t-form-item>
      <t-form-item label="个人简介" help="一句话介绍自己" name="description">
        <t-input v-model="formData.description"></t-input>
      </t-form-item>
      <t-form-item label="密码" name="password">
        <t-input type="password" v-model="formData.password"></t-input>
      </t-form-item>
      <t-form-item style="padding-top: 8px">
        <t-button theme="primary" type="submit" style="margin-right: 10px">提交</t-button>
        <t-button theme="default" variant="base" type="reset" style="margin-right: 10px">重置</t-button>
        <t-button theme="default" variant="base" @click="handleValidateMessage">设置校验信息提示</t-button>
      </t-form-item>
    </t-form>
  </div>
</template>
<script>
/* eslint-disable no-template-curly-in-string */
const INITIAL_DATA = {
  account: '',
  description: '',
  password: '',
};

const validateMessage = {
  account: [
    {
      type: 'error',
      message: '自定义用户名校验信息提示',
    },
  ],
  description: [
    {
      type: 'warning',
      message: '自定义个人简介校验信息提示',
    },
  ],
};

export default {
  data() {
    return {
      formData: { ...INITIAL_DATA },
      validateMessage,
      rules: {
        account: [{ required: true }, { min: 2 }, { max: 10, type: 'warning' }],
        description: [{ validator: (val) => val.length < 10, message: '不能超过 20 个字，中文长度等于英文长度' }],
        password: [{ required: true }, { len: 8, message: '请输入 8 位密码' }],
      },
    };
  },
  mounted() {
    this.$refs.form.setValidateMessage(validateMessage);
  },
  methods: {
    onReset() {
      this.$message.success('重置成功');
    },
    onSubmit({ validateResult, firstError }) {
      if (validateResult === true) {
        this.$message.success('提交成功');
      } else {
        console.log('Errors: ', validateResult);
        this.$message.warning(firstError);
      }
    },
    handleValidateMessage() {
      this.$message.success('设置表单校验信息提示成功');
      this.$refs.form.setValidateMessage(validateMessage);
    },
  },
};
</script>

<style scoped>
.demo-select-base {
  width: 300px;
}
</style>
