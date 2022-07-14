<template>
  <section class="section">

<!--   {{jobsall}} -->

<div v-for="item in jobsall">
<job 
v-bind:title="item.title"
v-bind:location="item.Location"
v-bind:description="item.Description"
/>
</div>


<job title="item.title"/>


</div>
    </div>
  </section>
</template>


 <script>
import Card from '~/components/Card'
import Job from '~/components/Job'
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
            jobsall:[]
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
