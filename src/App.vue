<template>
  <h1>hii</h1>
  <list-users />
  <create-user />
  <get-cookie />
  <protected-route-test />
</template>

<script>
import ListUsers from './components/api/ListUsers.vue'
import CreateUser from './components/api/CreateUser.vue'
import GetCookie from './components/api/GetCookie.vue'
import ProtectedRouteTest from './components/api/ProtectedRouteTest.vue'



export default {
  name: 'App',
  components: {
    ListUsers,
    CreateUser,
    GetCookie,
    ProtectedRouteTest,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
