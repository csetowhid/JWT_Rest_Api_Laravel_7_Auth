<template>
	<div>
	<div class="row justify-content-center">

      <div class="col-xl-10 col-lg-12 col-md-9">

        <div class="card o-hidden border-0 shadow-lg my-5">
          <div class="card-body p-0">
            <!-- Nested Row within Card Body -->
            <div class="row">
              <div class="col-lg-2"></div>
              <div class="col-lg-8">
                <div class="p-5">
                  <div class="text-center">
                    <h1 class="h4 text-gray-900 mb-4">Welcome Back!</h1>
                  </div>
                  <form class="user" @submit.prevent="login">
                    <div class="form-group">
                      <input type="email" class="form-control form-control-user" id="exampleInputEmail" aria-describedby="emailHelp" placeholder="Enter Email Address..." v-model="form.email">
                      <small class="text-danger" v-if="errors.email">{{errors.email[0]}}</small>
                    </div>
                    <div class="form-group">
                      <input type="password" class="form-control form-control-user" id="exampleInputPassword" placeholder="Password" v-model="form.password">
                      <small class="text-danger" v-if="errors.password">{{errors.password[0]}}</small>
                    </div>
                    <button class="btn btn-primary btn-user btn-block text-white">
                      Login
                    </button> 
                  </form>
                  <hr>

                  <div class="text-center">
                    <router-link to="/register">Create an Account!</router-link>
                  </div>
                </div>
              </div>
              <div class="col-lg-2"></div>
            </div>
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
        email:'',
        password:''
      },
      errors:{}
    }
  },
  methods:{
    login(){
      axios.post('/api/auth/login', this.form)
      .then(res => {
        User.responseAfterLogin(res)
        Toast.fire({
              icon: 'success',
              title: 'Signed in successfully'
            })
        this.$router.push({name: 'home'})
      })
      .catch(error => {
        this.errors = error.response.data.errors
        Toast.fire({
                icon: 'error',
                title: 'Invalid Email or Password'
              })
      })
    }
  }
}
</script>



<style>
	
</style>