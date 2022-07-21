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
            loggedinuser:[]
          }
        },



        computed: {

        },

        methods: {


addJob(jobname){
  const db = this.$fire.firestore;
  const data = {
'Budget':"100",
'Description': "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
'Location':"Dublin",
'Need by date':"22/4/2025",
'title':jobname
};
// let stampo = db.FieldValue.serverTimestamp();
// Add a new document in collection "cities" with ID 'LA'
const res = db.collection('jobs').doc('3').set(data);
}

        },


mounted () {
// this.getMarker();
this.addJob('Builder');

console.log('logged'+this.$fire.auth.currentUser);
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
