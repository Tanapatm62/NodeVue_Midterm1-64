<template>
  <div>
    <h1>Elephant</h1>
    <div v-if="users.length">
      <h4>จำนวนผู้ใช้งาน {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            สร้างข้อมูลช้าง
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>id: {{ user.id }}</p>
        <p>สายพันธุ์: {{ user.name }} - {{ user.lastname }}</p>
        <p>ลักษณะของช้าง: {{ user.email }}</p>
        <p>ข้อมูลช้าง: {{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            ดูข้อมูลช้าง
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูลช้าง
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูลช้าง
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>