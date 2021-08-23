<template>
  <div>
    <h1>Bicycle</h1>
    <div v-if="users.length">
      <h4>จำนวนจักรยานที่ลงทะเบียน {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            สร้างข้อมูลจักรยาน
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>id: {{ user.id }}</p>
        <p>ชื่อ: {{ user.name }} </p>
        <p>ราคา: {{ user.email }}</p>
        <p>หมายเลขผลิตภันฑ์:{{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            ดูข้อมูลจักรยาน
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูลจักรยาน
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูลจักยาน
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