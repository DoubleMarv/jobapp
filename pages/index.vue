<template>
  <section class="section">
  <Userbar :user="loggedinuser" />
<!--   {{jobsall}} -->

<div v-for="item in jobsall">
<job 
v-bind:title="item.title"
v-bind:location="item.Location"
v-bind:description="item.Description"
/>
</div>
Hey
<div v-for="job in makealldata.docs">
  {{job.id}}
</div>

  </section>
</template>


 <script>
import Card from '~/components/Card'
import Job from '~/components/Job'
import Userbar from '~/components/Userbar'
import { getFirestore, collection, query, where, getDocs } from "firebase/firestore";
      export default {

  name: 'IndexPage',
  components: {
    Card
  },


        head: {
          title: 'Job App',
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
            jobsall:[],
            loggedinuser:[],
            makealldata:[]
          }
        },


  async fetch() {
    const db = this.$fire.firestore;
    const docs = await db.collection('jobs').get();
docs.forEach (doc => {
    // console.log(`ID: ${doc.id}`);
    // console.log(doc.data());

this.jobsall.push(doc.data());
  });
  },

        computed: {

        },

        methods: {
        },


mounted () {
// this.getMarker();
if(this.$fire.auth.currentUser){
  this.loggedinuser = this.$fire.auth.currentUser
}

console.log('logged'+this.$fire.auth.currentUser);
},


created() {
    this.$nuxt.$on('getalldata', data => {
     this.makealldata = data._delegate
      })
    },
beforeDestroy() {
      // $off method will turn off the event listner
      this.$nuxt.$off('getalldata');
  },
// async getMarker() {
//   const db = this.$fire.firestore;
//     const snapshot = await db.firestore().collection('jobs').get()
//     const collection = {};
//     snapshot.forEach(doc => {
//         collection[doc.id] = doc.data();
//     });
//     return collection;
// }


};
</script>
