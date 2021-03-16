<template>
  <div id="app">
    <img class="logo" src="@/assets/LogoCompasso-positivo.png" alt="logo">
    
    <div class="container">
      <div class="card card-body">
        <p class="lead"> Type a name to find users and repositories</p>
        <input @keyup="getUser" id="search" type="text" class="form-control" required />
      </div> 
  
      <div class="row mt-3" v-if="user.length !== 0">
        <div class="col-md4">
          <Profile :user="user" />
        </div>

        <div class="col-md-6">
          <Repo v-for="repo in repos" :key="repo" :repo="repo"/>
        </div>
        
        <!-- <div class="card-body">
          <button v-on: click="getStarreds" class="btn btn-warning btn-block">Starreds</button>
          <button v-on: click="getRepos" class="btn btn-warning btn-block">Repos</button>
        </div> -->
      </div>
     </div>
  </div>
</template>

<script>
import Profile from "@/components/Profile.vue"
import Repo from "@/components/Repo.vue"
import axios from "axios"

export default {
  name: 'App',
    data() {
      return {
        github: {
          url: "https://api.github.com/users",
          cliente_id: "ec6748e0bcd334962de4",
          cliente_secret: "717a85dbf26772f6b4e352217018e7a12d105424",
          count: 7, 
          sort: "created: asc",
        },
        user: [],
        repos: [],
        repo: [],
        // starred: [],
      };
    },

  components: {
    Profile,
    Repo,
  },
  methods:{
    getUser(e){
      const user = e.target.value;
      const { url, cliente_id, cliente_secret, count, sort } = this.github;
      axios.get(
        `${url}/${user}?client_id=${cliente_id}&cliente_secret=${cliente_secret}`
      ).then(({ data }) => (this.user = data));

      axios.get(
          `${url}/${user}/repos?per_page=${count}&sort=${sort}&client_id=${cliente_id}&client_secret=${cliente_secret}`
        ).then(({ data }) => (this.repos = data));
      
      axios.get(
          `${url}/${user}/starred?per_page=${count}&sort=${sort}&client_id=${cliente_id}&client_secret=${cliente_secret}`
        ).then(({ data }) => (this.repos = data));
      },
  } 
}
</script>
<style> 
.logo{
  width: 40%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: black;
}
</style>
