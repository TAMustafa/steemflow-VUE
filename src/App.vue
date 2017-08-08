<template>
  <div class="container">
    <div class="jumbotron text-center">
    <h1>Steem - Flow</h1>
    <br>
    <form class="form-inline" v-on:submit.prevent>
        <button type="button" class="btn btn-default btn-lg" v-on:click="fromDir">
            <i class="fa fa-chevron-up" aria-hidden="true"></i> FROM </span>
        </button>
        <button type="button" class="btn btn-default btn-lg" v-on:click="toDir">
            <i class="fa fa-chevron-down" aria-hidden="true"></i> TO </span>
        </button>
        <input class="form-control input-lg" type="text" placeholder="Type Exchange or User..." v-model="exchname">
       
        <button type="button" class="btn btn-danger btn-lg" @click="submitted">
            <i class="fa fa-search" aria-hidden="true"></i> Get Data</button>
    
    </form>
    <br>
    <p id="btext"v-show="bclick"> Transactions <strong>{{direction}}</strong> {{exchname}} </p>

    <br>
    <i v-show="loading" class="fa fa-spinner fa-pulse fa-3x fa-fw"></i>
  </div>
   
   <app-search v-bind:results='results'></app-search>
   <app-nav></app-nav>

  </div>
</template>

<script>
import axios from 'axios';
import Search from './Search.vue'
import Navbar from './Navbar.vue'

export default {
    components: {
      appSearch: Search,
      appNav: Navbar
    },

    data: function() {
      return {
          direction:'',
          exchname: '',
          results: '',
          bclick: false,
          loading: false
      }
    },
    
    methods: {
        fromDir() {
          this.bclick = true;
          this.direction = 'from';
        },

        toDir() {
          this.bclick = true;
          this.direction = 'to';
        },

        submitted() {
            this.loading = true
            var vm = this
            axios.get('https://steemflow-exch-api.herokuapp.com/'+ vm.direction +'/' + vm.exchname)
            .then(function (response) {
              vm.results = response.data.exch
              vm.loading = false
            })
            .catch(function (error) {
              console.log(error);
        })
      }
    },
  }
</script>

<style scoped>
 #btext {
   color: rgb(41.2%, 41.2%, 41.2%);
 }

 h1{
   color: rgb(42.1%, 37.3%, 37.3%);
   font-family: 'Luckiest Guy', cursive;
 }

 .jumbotron {
   margin-top: 8%;
   
   background: white;
}

.fa-spinner  {
  color: rgb(87.8%, 35.9%, 35.9%);
}

.btn:hover  {
  background: rgb(87.8%, 35.9%, 35.9%);
}

</style>
