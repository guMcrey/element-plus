<template>
  <el-card shadow="hover" class="playground-container">
    <template #header>
      <el-link href="https://github.com/element-plus/element-plus/pull/10330">
        #10330
      </el-link>
      demo
    </template>
    <el-tabs v-model="activeName">
      <el-tab-pane label="validateTrim prop" name="a">
        <el-form :model="formA" :rules="formARule">
          <div class="container-title">Default</div>
          <el-form-item label="Username" prop="username1">
            <el-input v-model="formA.username1" />
          </el-form-item>
          <div class="container-title">Use validateTrim prop</div>
          <el-form-item label="Username" prop="username2" validate-trim>
            <el-input v-model="formA.username2" />
          </el-form-item>
        </el-form>
      </el-tab-pane>

      <el-tab-pane label="validateMsgUseLabel prop" name="b">
        <el-form :model="formB" :rules="formBRule">
          <div class="container-title">Default</div>
          <el-form-item label="Username" prop="username1">
            <el-input v-model="formB.username1" />
          </el-form-item>
          <div class="container-title">
            Use validateMsgUseLabel prop, and not custom rule message
          </div>
          <li class="container-sub-title">
            validateMsgUseLabel: <strong>boolean, true</strong>; label:
            <strong>exist</strong> -> label
          </li>
          <el-form-item
            label="Username"
            validate-msg-use-label
            prop="username2"
          >
            <el-input v-model="formB.username2" />
          </el-form-item>

          <li class="container-sub-title">
            validateMsgUseLabel: <strong>string</strong> -> validateMsgUseLabel
          </li>
          <el-form-item
            label="Username"
            validate-msg-use-label="Label name"
            prop="username3"
          >
            <el-input v-model="formB.username3" />
          </el-form-item>

          <li class="container-sub-title">
            validateMsgUseLabel: <strong>boolean, true</strong>; label:
            <strong>exist</strong>; use coustom message
          </li>
          <el-form-item
            label="Username"
            validate-msg-use-label
            prop="username4"
          >
            <el-input v-model="formB.username4" />
          </el-form-item>

          <li class="container-sub-title">
            validateMsgUseLabel: <strong>boolean, true</strong>; label:
            <strong>exist</strong>; use coustom validator
          </li>
          <el-form-item
            label="Username"
            validate-msg-use-label
            prop="username5"
          >
            <el-input v-model="formB.username5" />
          </el-form-item>
        </el-form>
      </el-tab-pane>
    </el-tabs>
  </el-card>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'
import type { FormRules } from 'element-plus'

const test = (rule: any, value: any, callback: any) => {
  if (value !== 'hello') {
    return callback(new Error('validator username5 custom message'))
  }
  callback()
}

const activeName = ref('a')
const formA = reactive({
  username1: '',
  username2: '',
})
const formARule = reactive<FormRules>({
  username1: {
    required: true,
    message: 'Username is required',
    trigger: ['blur', 'change'],
  },
  username2: {
    required: true,
    message: 'Username is required',
    trigger: ['blur', 'change'],
  },
})
const formB = reactive({
  username1: '',
  username2: '',
  username3: '',
  username4: '',
  username5: '',
})
const formBRule = reactive<FormRules>({
  username1: {
    required: true,
    trigger: ['blur', 'change'],
  },
  username2: {
    required: true,
    trigger: ['blur', 'change'],
  },
  username3: {
    required: true,
    trigger: ['blur', 'change'],
  },
  username4: {
    required: true,
    message: 'custome username4 rule message',
    trigger: ['blur', 'change'],
  },
  username5: [
    {
      required: true,
      trigger: ['blur', 'change'],
    },
    {
      validator: test,
      trigger: ['blur', 'change'],
    },
  ],
})
</script>

<style lang="scss">
.playground-container {
  width: 60%;
  margin: 0 auto 30px;
}
.container-title {
  margin: 20px 0;
  font-size: 14px;
  font-weight: 500;
  &:nth-child(3) {
    margin-top: 40px;
  }
}
.container-sub-title {
  margin: 30px 0 20px;
  font-size: 15px;
  color: #606060;
}
html,
body {
  width: 100vw;
  height: 100vh;
  margin: 10px;
  #play {
    height: 100%;
    width: 100%;
    .play-container {
      height: 100%;
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }
}
</style>
