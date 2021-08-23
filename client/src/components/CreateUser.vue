<template>
<div>
    <h1>สร้างข้อมูลช้าง</h1>
    <form v-on:submit.prevent = "createUser">
        <p>name: <input type="text" v-model="user.name"></p>
        <p>สายพันธุ์: <input type="text" v-model="user.lastname"></p>
        <p>ลักษณะของช้าง: <input type="text" v-model="user.email"></p>
        <p>ข้อมูลช้าง: <input type="text" v-model="user.password"></p>
        <p><button type="submit">create user</button></p>
    </form>
    <hr>
    <div>
        <p>name: {{user.name}}</p>
        <p>สายพันธุ์: {{user.lastname}}</p>
        <p>ลักษณะของช้าง: {{user.email}}</p>
        <p>ข้อมูลช้าง: {{user.password}}</p>
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