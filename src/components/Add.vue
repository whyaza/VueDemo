<template>
  <div class="add container">
    <h1 class="page-header">添加用户</h1>
    <form v-on:submit="addCustomer">
        <div class="well">
            <h4>用户信息</h4>
            <div class="form-group">
                <label for="">姓名</label>
                <input type="text" class="form-control" placeholder="name" v-model="customer.name">
            </div>
            <div class="form-group">
                <label for="">电话</label>
                <input type="text" class="form-control" placeholder="phone" v-model="customer.phone">
            </div>
            <div class="form-group">
                <label for="">邮箱</label>
                <input type="text" class="form-control" placeholder="email" v-model="customer.email">
            </div>
            <div class="form-group">
                <label for="">学历</label>
                <input type="text" class="form-control" placeholder="education" v-model="customer.education">
            </div>
            <div class="form-group">
                <label for="">毕业学校</label>
                <input type="text" class="form-control" placeholder="gradutionschool" v-model="customer.gradutionschool">
            </div>
            <div class="form-group">
                <label for="">职业</label>
                <input type="text" class="form-control" placeholder="profession" v-model="customer.profession">
            </div>
            <div class="form-group">
                <label for="">个人简介</label>
                <!-- <input type="text" class="form-control" placeholder="profile" v-model="customer.profile">-->
                <textarea class="form-control" rows="10" v-model="customer.profile"></textarea>
            </div>
            <button type="submit" class="btn">添加用户</button>
        </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
        customer:{}
    }
  },
  methods:{
      addCustomer(e){
          //console.log(123);
          if (!this.customer.name || !this.customer.phone || !this.customer.email){
            console.log("请添加对应的信息");
          }else{
            let newCustomer = {
                name: this.customer.name,
                phone: this.customer.phone,
                email: this.customer.email,
                education: this.customer.education,
                gradutionschool: this.customer.gradutionschool,
                profession: this.customer.profession,
                profile: this.customer.profile
            }

            this.$http.post("http://localhost:3000/users",newCustomer).then(function (response) {
                //this.$router.push({path: "/"});
                this.$router.push({path: "/", query:{alert: "用户信息添加成功！"}});
                //$router对象是全局路由的实例，是router构造方法的实例。
            });
            e.preventDefault(); //该方法将通知 Web 浏览器不要执行与事件关联的默认动作（如果存在这样的动作）
          }
          e.preventDefault();
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>