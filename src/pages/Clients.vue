<template>
  <div class="wrapper">
    <h1 id="title">{{title}}</h1>
    <h2>users database</h2>
  <div class="clients">
    <div class="container">
    <div class="user"  v-for="user in users" @click="slide(user)" :key="user.id">
      <ul>
        <li>name: {{user.name}}</li>
        <li>email: {{user.email}}</li>
        <li>phoneNumber: {{user.phone}}</li>
      </ul>
    </div>
  </div>
    <div class="content">
    <div class="circle" v-for="user in users" :key="user.name">
      <h1 class="namings">{{user.name}}</h1>
    </div>
  </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'users',
  data(){
    return{
      title: 'Vue users',
      usersURL:'https://jsonplaceholder.typicode.com/users',
      users:[],
      errors:[]
    }
  },
  mounted() {
    this.getUsers();
    // console.log(this.users[1])
  },methods:{
    slide (user){
      console.log(user.id)

    },
    async getUsers(){
      try {
        const response=await fetch(this.usersURL);
        const result=await response.json();
        this.users.push(...result)
        console.log(this.users[1])
      }catch (e){
        this.errors.push(e)
        console.log(e)
      }
    },getInformation(){
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.namings{
  font-weight: 100;
  width: 200px;
}
#title{
  font-size: 100px;
}
.content{

}
.clients{
  display: flex;

}
.circle{
  overflow: hidden;
  cursor: pointer;
  height: 100px;
  width: 60%;
  background-color: antiquewhite;
  border:solid 2px grey;
  transition: all .5s cubic-bezier(0.68, -0.55, 0.265, 1.55);


}
.circle:hover{
  width: 100%;
}
.container{
  display: flex;
  flex-direction: column;
  flex: 10;
}
*{
  margin: 5px;
}
.user{
  background-color: teal;
  width: 100%;
  flex: 1;
  border-radius: 20px;
  overflow: hidden;
}
.user.active{
  flex: 10;
  opacity: 0;
}

</style>
