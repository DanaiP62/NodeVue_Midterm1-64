<template>
  <div>
    <h1>ดูข้อมูลจักรยาน</h1>
    <p>id: {{ user.id }}</p>
    <p>ชื่อ:{{ user.name }} - {{ user.lastname }}</p>
    <p>ราคา:{{ user.email }}</p>
    <p>หมายเลขผลิตภันฑ์: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>