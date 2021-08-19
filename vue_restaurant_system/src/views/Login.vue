<template>
    <div>
        <el-card style="width:50%;margin: auto;">
            <h2>Login</h2>
            <el-form
            :model="model"
            :rules="rules"
            ref="form"
            @submit.prevent="login"
            >
                <el-form-item prop="account">
                    <el-input 
                    v-model="model.account"
                    placeholder="Account"
                    prefix-icon="el-icon-user-solid"
                    ></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input
                    v-model="model.password"
                    placeholder="Password"
                    type="password"
                    prefix-icon="el-icon-lock"
                    ></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button
                    :loading="loading"
                    type="primary"
                    native-type="submit"
                    >Login
                    </el-button>
                </el-form-item>
            </el-form>
            <p>{{successMsg}}</p>
        </el-card>
    </div>
</template>

<script>

export default{
    data(){
        return{
            successMsg:"No yet login!",
            loading : false,
            validCredentials:{
                account : "vinson",
                password : "vinson666"
            },
            model:{
                account : "",
                password : "",
            },
            rules:{
                account:[
                    {
                        required : true,
                        message : "Account is required",
                        trigger : "blur"
                    },
                    {
                        min : 4,
                        message: "User should input at least 4 digits",
                        trigger: "blur"
                    }
                ],
                password:[
                    {
                        required : true,
                        message : "Password is required",
                        trigger: "blur"
                    },
                    {
                        min : 5,
                        message : "User should input at least 5 digits",
                        trigger : "blur"
                    }
                ]
            }

        }
    },
    methods: {
        simulateLogin() {
        return new Promise(resolve => {
            setTimeout(resolve, 1000);
        });
        },
        delay() {
            setTimeout(()=>{this.successMsg = "Successfully!"}, 5000);
        },
        async login() {
        let valid = await this.$refs.form.validate();
        if (!valid) {
            return;
        }
        this.loading = true;
        this.delay();
        await this.simulateLogin();
        this.loading = false;
        if (
            this.model.account === this.validCredentials.account &&
            this.model.password === this.validCredentials.password
        ) {
            this.$message.success("Login successfull");
        } else {
            this.$message.error("Username or password is invalid");
        }
        }
  }
}
</script>
