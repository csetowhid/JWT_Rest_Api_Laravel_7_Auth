<template>
	<div>
<div class="container">
    <div class="card o-hidden border-0 shadow-lg my-5">
      <div class="card-body p-0">
        <!-- Nested Row within Card Body -->
        <div class="row">
          <div class="col-lg-2"></div>
          <div class="col-lg-8">
            <div class="p-5">
              <div class="text-center">
                <h1 class="h4 text-gray-900 mb-4">Create an Account!</h1>
              </div>
              <form class="user" @submit.prevent="signup">
                <div class="form-group">
                    <input type="text" class="form-control form-control-user" placeholder="Enter Name" v-model="form.name">
                    <small class="text-danger" v-if="errors.name">{{errors.name[0]}}</small>
                </div>
                <div class="form-group">
                  <input type="email" class="form-control form-control-user" id="exampleInputEmail" placeholder="Email Address" v-model="form.email">
                  <small class="text-danger" v-if="errors.email">{{errors.email[0]}}</small>
                </div>
                <div class="form-group row">
                  <div class="col-sm-6 mb-3 mb-sm-0">
                    <input type="password" class="form-control form-control-user" id="exampleInputPassword" placeholder="Password" v-model="form.password">
                    <small class="text-danger" v-if="errors.password">{{errors.password[0]}}</small>
                  </div>
                  <div class="col-sm-6">
                    <input type="password" class="form-control form-control-user" id="exampleRepeatPassword" placeholder="Repeat Password" v-model="form.password_confirmation">
                  </div>
                </div>
                <button class="btn btn-primary btn-user btn-block">
                      Register Account
                </button> 
              </form>
              <hr>
              <div class="text-center">
                <router-link class="small" to="/">Already have an account? Login!</router-link>
              </div>
            </div>
          </div>
          <div class="col-lg-2"></div>
        </div>
      </div>
    </div>

</div>
	</div>
</template>

<script>
export default{
  created(){
    if(User.loggedIn()){
      this.$router.push({name: 'home'})
    }
  },
  data(){
    return {
      form:{
        name:'',
        email:'',
        password:'',
        confirm_password:''
      },
      errors:{}
    }
  },
  methods:{
    signup(){
      axios.post('/api/auth/signup', this.form)
      .then(res => {
        User.responseAfterLogin(res)
        Toast.fire({
              icon: 'success',
              title: 'Sign Up Successfully'
            })
        this.$router.push({name: 'home'})
      })
      .catch(error => {
        this.errors = error.response.data.errors
        // Toast.fire({
        //         icon: 'error',
        //         title: 'Invalid Email or Password'
        //       })
      })
    }
  }
}
</script>

<style>
	
</style>