// Home.vue

<template>
  <div>
    <p>Home page</p>
    <p>Random number from backend: {{ randomNumber }}</p>
    <button @click = "getRandom">New random number</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data(){ 
    return{
      randomNumber: 0
    }
  },
  methods: {
    getRandomInt(min,max){
      min=Math.ceil(min)
      max=Math.floor(max)
      return Math.floor(Math.random() * (max-min +1))+min
    },
    getRandomFormBackend(){
      const path ='http://35.190.195.31/api/random'
      axios.get(path)
        .then(response=>{
          this.randomNumber=response.data.randomNumber
        })
        .catch(error =>{
          console.log(error)
        }
        )
    },
    getRandom() { 
      // this.randomNumber = this.getRandomInt(1,100)
      this.randomNumber=this.getRandomFormBackend()
    }
  },
  created () {
    this.getRandom()
  }
}
</script>
