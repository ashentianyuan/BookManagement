<template>
    <div>
        <div class="el-form-container">
            <div class="login-text">登录简单图书管理系统</div>
            <el-form ref="form" :model="form" :rules="rules" label-width="70px" class="el-form">
                <el-form-item label="用户名" prop="userName">
                    <el-input v-model="form.userName" placeholder="请输入用户名" prefix-icon="el-icon-user-solid"/>
                </el-form-item>
                <el-form-item label="密码" prop="password">
                    <el-input v-model="form.password" placeholder="请输入密码" show-password
                              prefix-icon="el-icon-s-promotion"/>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit" class="login-button">登录</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
    import {Message} from "element-ui"

    export default {
        name: "login",
        data() {
            return {
                form: {
                    userName: "",
                    password: ""
                },
                rules: {
                    userName: [
                        {required: true, message: '请输入用户名', trigger: 'blur'},
                        {min: 3, max: 20, message: '长度在 3 到 20 个字符', trigger: 'blur'}
                    ],
                    password: [
                        {required: true, message: '请输入密码', trigger: 'blur'},
                        {min: 3, max: 20, message: '长度在 3 到 20 个字符', trigger: 'blur'}
                    ],
                }
            }
        },
        methods: {
            onSubmit: function () {
                this.$api({
                    method: 'post',
                    url: '/Login',
                    data: {
                        name: this.form.userName,
                        password: this.form.password
                    }
                }).then(res => {
                    Message({
                        message: res.message,
                        type: 'success',
                        duration: 5 * 1000
                    });
                })
            }
        }
    }
</script>

<style scoped>
    .login-button {
        width: 80%;
    }

    .login-text {
        font-size: 1.8em;
        line-height: 3em;
        text-align: center;
    }

    .el-form {
        width: 70%;
        margin: 0 auto;
    }

    .el-form-container {
        box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
        background-color: white;
        padding: 10px;
        max-width: 400px;
        margin: 150px auto 0;
    }

</style>