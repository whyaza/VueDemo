<template>
  <div class="customers container">
    <alert v-if="alert" v-bind:message="alert"></alert>
    <h1 class="page-header">用户管理系统</h1>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th>详情</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="customer in customers" :key="customer.id">
          <td>{{ customer.name }}</td>
          <td>{{ customer.phone }}</td>
          <td>{{ customer.email }}</td>
          <td><router-link class="btn btn-default" v-bind:to="'/customer/'+customer.id">详情</router-link></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Alert from './alert'
export default {
  name: 'customers',
  data () {
    return {
      customers:[],
      alert:"",
    }
  },
  methods:{
    fetchCustomers(){
      this.$http.get("http://localhost:3000/users")
          .then(function (response){
            //console.log(response);
            this.customers = response.body;
          })
    }
  },
  created(){
    if (this.$route.query.alert){
      this.alert = this.$route.query.alert;
    } //$route对象表示当前的路由信息，包含了当前 URL 解析得到的信息。包含当前的路径，参数，query对象等。
    this.fetchCustomers();
  },
  updated(){
    this.fetchCustomers();
  },
  components:{
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
