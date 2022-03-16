<template>
  <div id="app">
    <ul>
      <li v-for="item in items" :key="item.id">
        {{item.first_name}} <br>
        <img :src="item.avatar">  
      </li>
    </ul>
    <input type="text" v-model="name">
    <input type="text" v-model="job">
    <button @click="sendUser">Add User</button>
    <hr>
    <input type="text" v-model="id">
    <button @click="deleteUser">Delete User</button>
    <hr>
    
    <input type="text" v-model="name">
    <input type="text" v-model="job">
    <input type="text" v-model="id">
    <button @click="updateUser">Update User</button>
  </div>
</template>

<script>

export default {
  data() {
    return {
      items:[],
      name :'',
      job :'',
      id:null,
    }
  },
  methods: {
    sendUser() {
      this.$http.post('https://reqres.in/api/users', {name:this.name, job:this.job})
      .then(response=>{
        console.log(response.body);
      })
    },
    deleteUser() {
      this.$http.delete('https://reqres.in/api/users/',+this.id)
      .then(response=>{
        console.log(response);
      })
    },
    updateUser() {
      this.$http.put('https://reqres.in/api/users/'+this.id, {name:this.name, job:this.job})
      .then(response=>{
        console.log(response);
      })
    }
  },
  beforeCreate() {
    {
  // GET /someUrl
  this.$http.get('https://reqres.in/api/users').then(response => {
    this.items.push(...response.body.data)
    console.log(response.body.data);

  }, response => {
    console.log(response.body.data);
  });
}
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
