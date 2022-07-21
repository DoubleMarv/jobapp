<template>
  <div>
    <b-navbar>
        <template #brand>
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                <img
                    src="https://raw.githubusercontent.com/buefy/buefy/dev/static/img/buefy-logo.png"
                    alt="Lightweight UI components for Vue.js based on Bulma"
                >
            </b-navbar-item>
        </template>
        <template #start>

<NuxtLink v-if="loggedin" to="/login" class="navbar-item">
    Logout Bitch
</NuxtLink>
<NuxtLink v-else to="/login" class="navbar-item">
    Login
</NuxtLink>


<NuxtLink v-if="loggedin" to="/addjob" class="navbar-item">
    Add a job
</NuxtLink>
            <b-navbar-item href="#">
                Documentation
            </b-navbar-item>
            <b-navbar-dropdown label="Info">
                <b-navbar-item href="#">
                    Contact
                </b-navbar-item>
            </b-navbar-dropdown>
        </template>

        <template #end>
          <NuxtLink to="/login" class="navbar-item is-primary">
    Login
</NuxtLink>
<NuxtLink v-if="loggedin" to="/addjob" class="navbar-item is-light">
    Add a job
</NuxtLink>
        </template>
    </b-navbar>

    <section class="main-content columns">
      <aside class="column is-2 section">
        <p class="menu-label is-hidden-touch">
          General
        </p>
        <ul class="menu-list">
          <li
            v-for="(item, key) of items"
            :key="key"
          >
            <NuxtLink
              :to="item.to"
              exact-active-class="is-active"
            >
              <b-icon :icon="item.icon" /> {{ item.title }}
            </NuxtLink>
          </li>
        </ul>
      </aside>
      <div class="container column is-10">
        <Nuxt :alldata="everything"/>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      loggedin:false,
      everything:[],
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' }
        }
      ]
    }
  },

methods: {

},

  mounted () {
if(this.$fire.auth.currentUser){
  let loggo = this.$fire.auth.currentUser;
  this.loggedin = true
}else{
    this.loggedin = false
}

console.log('logged'+this.$fire.auth.currentUser);
},

  async fetch() {
    const db = this.$fire.firestore;
    this.everything = await db.collection('jobs').get();
    if(this.everything){
        this.$nuxt.$emit('getalldata', this.everything); 
    }
  },


}
</script>
