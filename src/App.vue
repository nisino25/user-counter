<template>
  <h1>hey</h1>
  <button @click="addData()">Click me</button>
  <h2 v-if="userNum !== 0">{{userNum}}</h2>
</template>

<script>
import db from "./firebase.js"
// import { doc, setDoc } from "firebase/firestore"; 
// import { doc, setDoc } from "firebase/firestore";

export default {
  data(){
    return{
      fireData:[],
      userNum: 0,
    }
  },

  methods:{
    readData(){
      console.log('je')
    },

    addData(){
      console.log('heeey')
      const ref = db.collection('user-counter')
      ref.doc('b6YDm6PykPYGfIKptNKt').update({
        TotalNum: this.userNum + 1
      })
    },

  },
  watch:{
    userNum(){
      console.log('just ogt data')
        const ref = db.collection('user-counter')
        ref.doc('b6YDm6PykPYGfIKptNKt').update({
          TotalNum: this.userNum 
        })
      console.log('Sent data now')
    }

  },

  mounted: function () {
   db.collection("user-counter")
     .get()
     .then((querySnapshot) => {
       querySnapshot.forEach((doc) => {
         console.log(`${doc.id} => ${doc.data().TotalNum}`)
         this.fireData.push(doc.data().TotalNum)
         this.userNum = doc.data().TotalNum + 1

       })
     })

  
  },
  


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
