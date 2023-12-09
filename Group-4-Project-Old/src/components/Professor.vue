<template>
    <div class='professor'>
        <div class="navbar">
            <div class="welcome">
                <p>{{ 'Welcome ' + currentUser }}</p>
            </div>
            <div class="button">
                <button @click="logOut()" type="button">Log out</button>
            </div>
        </div>  
    </div>
</template>

<script>
export default {
    props:['currentUser'],
    methods: {
        logOut() {
            this.$emit('logOut')
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
</style>