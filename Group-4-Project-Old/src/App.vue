<template>
    <Login :class="{hide: currentScreen!='Login'}" @changeScreen="changeScreen($event)"></Login>
    <Student 
        :class="{hide: currentScreen!='Student'}" 
        :current-user="currentUser" 
        :columns="columns"
        :classes="classes"
        @logOut="logOut()">
    </Student>   
    <Professor 
        :class="{hide: currentScreen!='Professor'}" 
        :current-user="currentUser" 
        @logOut="logOut()">
    </Professor> 
    <Admin 
        :class="{hide: currentScreen!='Admin'}" 
        :current-user="currentUser" 
        :columns="columns"
        @logOut="logOut()">
    </Admin> 
</template>

<script>
import Login from './components/Login.vue'
import Student from './components/Student.vue'
import Professor from './components/Professor.vue'
import Admin from './components/Admin.vue'

export default {
    data() {
        return {
            currentUser: '',
            currentScreen: 'Login',
            screens: ['Login', 'Student', 'Professor', 'Admin'],
            backgroundColors: ['#000E90', 'white'],
            columns: ['Subject', 'Class ID', 'Name', 'Number', 'Professor', 'Credits', 'Mon', 'Tue', 'Wed', 'Thr', 'Fri'],
            classes: [
                {'Subject': 'Math', 'Class ID': '1', 'Name': 'Linear Algebra', 'Number': '2000', 'Professor': 'John Smith', 'Credits': '3', 'Days': 'Tue/Thr'},
            ],
            newClass: ''
        }
    },
    components: {
        Login,
        Student,
        Professor,
        Admin
    },
    methods: {
        changeScreen(data) {
            this.currentScreen = data.group
            this.currentUser = data.user
            document.body.style.backgroundColor = this.backgroundColors[1]
        },
        logOut() {
            this.currentScreen = 'Login'
            document.body.style.backgroundColor = this.backgroundColors[0]
        },
        addClass(classObj) {
            this.classes.push(classObj)
        }
    }
}
</script>

<style>
body{
    background-color: #000E90;
}
.login{
    background-color: white;
    width: 473px;
    height: 350px;
    margin: 75px auto;
    text-align: center;
}
.login.hide{
    display: none;
}
.student.hide{
    display: none;
}
.professor.hide{
    display: none;
}
.admin.hide{
    display: none;
}
</style>