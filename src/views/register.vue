<template>
  <div class="registerPage">
    <div class="registerCard">
        <div class="registerCardLeft">

        </div>
        <div class="registerCardRight">
            <div class="registerFormHead">
                <h1>Register</h1>
            </div>
            <div class="registerForm">
                <form @submit.prevent="register">
                    <label for="email">Email</label>
                    <input type="email" placeholder="Insert email" name="email" id="email" style="margin: 3% 0;" v-model="email">
                    <label for="password">Password</label>
                    <input type="password" placeholder="Insert password" name="password" id="password" style="margin: 3% 0;" v-model="password">
                    <button type="submit" style="margin: 3% 0;">Register</button>
                    <button type="submit" style="margin: 3% 0;" @click="$emit('loginback')">Login</button>
                </form>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name:"RegisterPage",
    data() {
        return{
            email: '',
            password: ''
        }
    },
    methods: {
        register() {
            axios({
            method:"POST",
            url: "https://ancient-mesa-33338.herokuapp.com/user/signup",
            data:{
                email: this.email,
                password: this.password
            }
        })
        .then(({data}) => {
            localStorage.setItem('access_token',data.access_token)
            this.$toast.success('Yeay, Register success! Welcome to Kanban Board', {
                // optional options Object
                })
            this.$emit('login')
        }) 
        .catch(err => {
            console.log(err.response.data.errors[0].message)
            let error= err.response.data.errors[0].message
            this.$toast.error(error,{})
            })
        }
    }
}
</script>

<style>

</style>