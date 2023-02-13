<template>
  <div class="container" id="login-box">
    <div class="form-container sign-up-container">
      <el-form :rules="rules">
        <h1>注册</h1>
        <el-form-item class="txtb">
          <input type="text" v-model="register.username" id="in1" @focus="fo1" @blur="bl1">
          <span data-placeholder="Useranme"></span>
        </el-form-item>
        <el-form-item class="txtb">
          <input type="email" v-model="register.email" id="in2" @focus="fo2" @blur="bl2">
          <span data-placeholder="Email"></span>
        </el-form-item>
        <el-form-item class="txtb">
          <input type="password" v-model="register.password" id="in3" @focus="fo3" @blur="bl3">
          <span data-placeholder="Password"></span>
        </el-form-item>
        <el-form-item class="txtb" prop="confirm">
          <input type="password" v-model="register.confirm" id="in4" @focus="fo4" @blur="bl4">
          <span data-placeholder="Confirm Password"></span>
        </el-form-item>
        <button type="submit" @click="submitform1">注册</button>
      </el-form>
    </div>
    <div class="form-container sign-in-container">
      <el-form>
        <h1>登录</h1>
        <div class="txtb">
          <input type="email" v-model="login.email" id="input1" @focus="action1" @blur="action2">
          <span data-placeholder="Email"></span>
        </div>
        <div class="txtb">
          <input type="password" v-model="login.password" id="input2" @focus="action3" @blur="action4">
          <span data-placeholder="Password" id="span2"></span>
        </div>
        <a href="#">忘记密码？</a>
        <button type="submit" @click="submitform2">登录</button>
      </el-form>
    </div>

    <div class="overlay-container">
      <div class="overlay">
        <div class="overlay-panel overlay-left">
          <h1>已有账号？</h1>
          <p>请使用您的账号进行登录</p>
          <button class="ghost" id="signIn" ref="signIn" @click="show1">登录</button>
        </div>
        <div class="overlay-panel overlay-right">
          <h1>没有账号?</h1>
          <p>立即注册加入我们，和我们一起开始旅程吧</p>
          <button class="ghost" id="signUp" ref="signUp" @click="show2">注册</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import axios from 'axios'

const register = reactive({
  username: '',
  email: '',
  password: '',
  confirm: ''
})

const login = reactive({
  email: '',
  password: ''
})

const submitform1 = () => {
  axios.post('http://localhost:8082/register1/register', {
    username: register.username,
    email: register.email,
    password: register.password,
    confirm: register.confirm
  })
    .then(function (response) {
      console.log(response)
    })
    .catch(function (error) {
      console.log(error)
    })
}

const submitform2 = () => {
  axios.post('http://localhost:8082/register1/login', {
    email: login.email,
    password: login.password
  })
    .then(function (response) {
      console.log(response)
    })
    .catch(function (error) {
      console.log(error)
    })
}

const show1 = (evt: Event) => {
  document.getElementById('login-box')?.classList.remove('right-panel-active')
}
const show2 = (evt: Event) => {
  document.getElementById('login-box')?.classList.add('right-panel-active')
}

const action1 = (evt: Event) => {
  document.getElementById('input1')?.classList.add('focus')
}

const action2 = (evt: Event) => {
  if (login.email === '') {
    document.getElementById('input1')?.classList.remove('focus')
  }
}

const action3 = (evt: Event) => {
  document.getElementById('input2')?.classList.add('focus')
}

const action4 = (evt: Event) => {
  if (login.password === '') {
    document.getElementById('input2')?.classList.remove('focus')
  }
}

const fo1 = (evt: Event) => {
  document.getElementById('in1')?.classList.add('focus')
}

const bl1 = (evt: Event) => {
  if (register.username === '') {
    document.getElementById('in1')?.classList.remove('focus')
  }
}

const fo2 = (evt: Event) => {
  document.getElementById('in2')?.classList.add('focus')
}

const bl2 = (evt: Event) => {
  if (register.email === '') {
    document.getElementById('in2')?.classList.remove('focus')
  }
}

const fo3 = (evt: Event) => {
  document.getElementById('in3')?.classList.add('focus')
}

const bl3 = (evt: Event) => {
  if (register.password === '') {
    document.getElementById('in3')?.classList.remove('focus')
  }
}

const fo4 = (evt: Event) => {
  document.getElementById('in4')?.classList.add('focus')
}

const bl4 = (evt: Event) => {
  if (register.confirm === '') {
    document.getElementById('in4')?.classList.remove('focus')
  }
}
</script>

<style type="text/css">
@import "/src/style/register.css";
</style>
