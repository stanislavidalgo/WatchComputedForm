<template>
  <div id="app">

    <input type="text" placeholder="name" :class="valids[0] ? 'valid' : 'invalid' " v-model="name">
    <input type="text" placeholder="surname" :class="valids[1] ? 'valid' : 'invalid' " v-model="surname">
    <input type="text" placeholder="city" :class="valids[2] ? 'valid' : 'invalid' " v-model="city">
    <input type="text" placeholder="age" :class="valids[3] ? 'valid' : 'invalid' " v-model="age">

    <h4>{{formText}}</h4>
    <button @click="checkValid" :class="[allvalid ? '' : 'invalid']">Accept</button>

    <Demo/>
  </div>
</template>

<script>
import Demo from './components/Demo.vue'


export default {

  name: 'App',

  components: {
    
  },

  data(){
    return {
      name:"",
      surname:"",
      city:"",
      age:"",
      valids:[true,true,true,true],
      allValid: true
    }
  },
  methods:{
    checkValid(){
      this.allValid = true
      this.valids.map(item => item ? null : this.allValid = false)
    }
  },
  watch:{
    name:function(newName){

      this.valids[0] = !(newName.length > 20 || newName.length < 3)

      //or like this

      // if(newName.length > 20 || newName.length < 3){
      //   this.valids[0] = false
      // }else{
      //   this.valids[0] = true 
      // }
    },
    surname:function(newSurname){
      if(newSurname.length > 20 || newSurname.length < 3){
        this.valids[1] = false
      } else {
        this.valids[1] = true 
      }
    },
    city:function(newCity){
      if(newCity.length > 20 || newCity.length < 3){
        this.valids[2] = false
      } else {
        this.valids[2] = true 
      }
    },
    age:function(newAge){
      if(newAge.length > 20 || newAge.length < 3){
        this.valids[3] = false
      } else {
        this.valids[3] = true 
      }
    },

  },
  computed:{
    formText(){
      return `my name is ${this.name} ${this.surname}, I am from ${this.city}, and I am ${this.age} years old`
    }
  }
}
</script>



<style>

body{
  margin: 50px;
  font-family: monospace;
}

#app {
  display: flex;
  flex-direction: column;
  padding: 50px;
  width: 400px;
  background-color: #f1f1f1;
}

.invalid{
  border: 2px solid rgba(195, 71, 71, 0.664);
}

.valid{
  border: 2px solid rgba(56, 151, 56, 0.746);
}
</style>
