<template>
  <div class="mb-6">
    <section class="hero is-medium is-primary is-bold mb-6" >
      <div class="hero-body">
        <div class="container has-text-centered column is-three-quarters">
          <h1 class="title">GitHub Repo Generator</h1>
          <h2 class="subtitle">Get all your repositories within seconds.</h2>
          
        </div>
        <div class="container has-text-centered column is-one-third">
            <input class="input is-rounded" v-model="myusername" type="text" placeholder="Enter your Github Username">
             <button class="button is-primary is-rounded mt-4" v-on:click="getRepoDetail">
          Fetch Data
        </button>
        </div>
      </div>
    </section>
    <div class="container">
      <div class="table-container">
        <table class="table is-bordered is-striped is-hoverable is-fullwidth">
          <thead>
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>URL</th>
              <th>Language</th>
              <th>Login</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="repo in repos" :key="repo.id">
              <td>{{repo.id}}</td>
              <td>{{repo.name}}</td>
              <td><a :href="repo.html_url">{{repo.html_url}}</a></td>
              <td>{{repo.language}}</td>
              <td>{{repo.owner.login}}</td>
            </tr>       
          </tbody>
        </table>
      </div>
    </div>
    
  <div class="content has-text-centered is-vcentered mt-6">
    <p>
      <strong>Made with VueJs</strong> by <a href="https://github.com/Rohanfulzele">Rohan Fulzele</a>. 
    </p>
  </div>
  
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: "Repository",
  data(){
    return{
      repos:null,
      myusername:null
    };
  },
  methods: {
  getRepoDetail:function(){
      axios.get('https://api.github.com/users/'+this.myusername+'/repos').then((response) => {
      this.repos = response.data;
      });
    }
  }
};
</script>

<style>
body {
  font: 15px/1.8 "Poppins", sans-serif !important;
}

.table td,
.table th {
  padding: 20px !important;
}
</style>