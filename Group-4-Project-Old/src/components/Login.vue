<template>
    <div class="login">
        <div class="login_button_div">
            <div v-for="group in groups">
                <button @click="changeGroup(group)" class="login_button" type="button">{{ group }}</button>
            </div>
        </div>
    
        <h1>University {{ activeGroup }} Login</h1>
    
        <form>
            <div class = user_div>
                <label for="username">Username:</label><br>
                <input v-model="currentUser" id="username" name="username"><br>
            </div>
            <div class="pass_div">
                <label for="password">Password:</label><br>
                <input v-model="password" type="password" id="password" name="password"><br><br>
            </div>
            <button @click="loginCheck()" type="button">Login</button>
            <p>{{ message }}</p>
        </form> 
    </div>
</template>

<script>
export default {
    data() {
        return {
            currentUser: '',
            password: '',
            activeGroup: 'Student',
            groups: ['Student', 'Professor', 'Admin'],
            message: ''
        }
    },
    methods: {
        changeGroup(newGroup) {
            this.activeGroup = newGroup
        },
        loginCheck() {
            if (this.currentUser == '') {
                this.message = 'Please Enter Username'
                this.password=''
            }
            else {
                this.changeScreen()
            }
        },
        changeScreen() {
            this.$emit('changeScreen', {group: this.activeGroup, user: this.currentUser})
            this.message=''
            this.currentUser=''
        }
    }
}
</script>

<style>

.login_button_div{
    display: flex;
    justify-content: center;
}

.login_button{
    padding: 10px 54px;
}

.user_div{
    padding: 15px 15px 2.5px 15px;
}

.pass_div{
    padding: 2.5px 15px 5px 15px;
}
</style>