<template>
  <section class="section">
    <h2 class="title is-3 has-text-grey">
Login
    </h2>
<a class="button" @click="login()">Login</a>
  </section>
</template>

<script>
  import { getAuth  } from "firebase/auth";

      export default {
  name: 'InspirePage',
  // components: {
  //   Card
  // },

        head: {
          title: 'Login Page',
          meta: [
          {
            hid: 'description',
            name: 'description',
            content: 'This is the ses'
          }
          ],
        },
        data() {
          return {
            // jobsall:[]
          }
        },

        computed: {

        },

        methods: {
login(){
  let self = this;
  const provider = new $nuxt.$fireModule.auth.GoogleAuthProvider()
   this.$fire.auth.signInWithPopup(provider)
   .catch(function(error){
    console.log(error.message);
   }).then((user)=>{
    //we are signed in
    console.log(user);
    // $nuxt.$router.push('/cumfarts');
   })
},
        },


mounted () {
// this.getMarker();
},



};


</script>
