<template>
    <div class='student'>
        <div class="navbar">
            <div class="welcome">
                <p>{{ 'Welcome ' + currentUser }}</p>
            </div>
            <div class="button">
                <button @click="logOut()" type="button">Log out</button>
            </div>
        </div>  

        <div class='student-body'>
            <form class="api-get-input">
                <p>Search for Class Subject:</p>
                <input class="subject-search" type="query" v-model="subject">
                <button type="button" @click="getSubjectCheck">Search</button>
            </form>
            <form class="search">
                <p>Search for Classes:</p>
                <input class="class-search" type="query" v-model="searchQuery">
            </form>
            <StudentGrid @addClass="addClass($event)" :data="classes" :columns="columns" :filter-key="searchQuery"></StudentGrid>
            <p>{{ userClasses }}</p>
        </div>
    </div>
</template>

<script>
import StudentGrid from './StudentGrid.vue'

export default {
    data() {
        return {
            classes: [],
            userClasses: [],
            searchQuery: '',
            subject: '',
            currentSubject: ''
        }
    },
    components: {
        StudentGrid
    },
    props:['currentUser', 'columns'],
    methods: {
        logOut() {
            this.classes = []
            this.userClasses = []
            this.$emit('logOut')
        },
        async getSubject() {
            let url = "https://yhw30hsvu5.execute-api.us-east-1.amazonaws.com/classes/dynamodbmanager?subject=" + this.subject
            this.currentSubject = this.subject
            this.subject = ''
            const response = await fetch(url)
            const classL = await response.json()
            this.classes = []
            for (let i = 0; i < classL.Count; i++) {
                const newClass = {
                    'Subject': classL.Items[i].Subject.S,
                    'Class ID': classL.Items[i].ClassId.S,
                    'Name': classL.Items[i].name.S,
                    'Number': classL.Items[i].number.S,
                    'Professor': classL.Items[i].professor.S,
                    'Credits': classL.Items[i].credits.S,
                    'Mon': classL.Items[i].mon.S,
                    'Tue': classL.Items[i].tue.S,
                    'Wed': classL.Items[i].wed.S,
                    'Thr': classL.Items[i].thr.S,
                    'Fri': classL.Items[i].fri.S,
                }
                this.classes.push(newClass)
                this.classes.sort((a, b) => a.Number - b.Number);
            }
        },
        getSubjectCheck() {
            if (this.subject != '' && this.subject != this.currentSubject) {
                console.log('Getting', this.subject)
                this.getSubject()
            }
        },
        addClass(ClassId) {
            this.userClasses.push(this.classes.filter(classObj => classObj['Class ID'] === ClassId))
            console.log(this.userClasses)
        }
    }
}
</script>

<style>
.navbar{
    display: flex;
    align-items: baseline;
    background-color: #000E90;
}
.welcome{
    color: white;
    font-size: 20px;
    text-align: center;
    padding: 10px 10px;
    text-decoration: none;
}
.button{
    margin-left: auto;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
}
.search{
    padding-bottom: 8px;
}
.search p{
    margin: 8px 0 0 0;
}
</style>
