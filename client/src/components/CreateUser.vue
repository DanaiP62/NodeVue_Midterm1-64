<template>
<div>
    <h1>สร้างข้อมูลจักรยาน</h1>
    <form v-on:submit.prevent = "createUser">
        <p>ชื่อ: <input type="text" v-model="user.name"></p>
        <p>ราคา: <input type="text" v-model="user.email"></p>
        <p>หมายเลขผลิตภันฑ์: <input type="text" v-model="user.password"></p>
        <p><button type="submit">create</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อ: {{user.name}}</p>
        <p>ราคา: {{user.email}}</p>
        <p>หมายเลขผลิตภันฑ์:: {{user.password}}</p>
    </div>
</div>
</template>
<script>
import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async createUser(){
            try{
                await UsersService.post(this.user)
                this.$router.push({
                    name: 'users'
                })
            }catch(error){
                console.log(error)
            }
        }
    }    
}
</script>
<style scoped>


</style>