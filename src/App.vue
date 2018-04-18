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

        <input class="form-control input-lg" type="text" placeholder="Enter account name" v-model="accountname">

        <button type="button" class="btn btn-danger btn-lg" @click="validate">
          <i class="fa fa-search" aria-hidden="true"></i> Submit</button>

      </form>
      <br>
      <h4> {{msgCompleteFields}} </h4>
      <h4> {{msgNoResults}} </h4>

      <br>

      <div v-show="loading">
        <i class="fa fa-spinner fa-pulse fa-3x fa-fw"></i>
        <p> {{ loadingmessage }} </p>
      </div>

    </div>

    <app-search v-bind:results='results' v-bind:direction='direction' v-bind:accountname='accountname'></app-search>
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

    data: function () {
      return {
        direction: '',
        accountname: '',
        results: [],
        bclick: false,
        loading: false,
        loadingmessage: 'Fetching results from SteemData',
        msgCompleteFields: '',
        msgNoResults: ''
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

      validate() {
        if (this.bclick == true && this.accountname.length > 0) {
          this.submitted()
        } else {
          this.msgCompleteFields = "Please enter From / To and account name"
          this.accountname = ''
        }
      },

      submitted() {
        this.loading = true
        this.message1 = ''
        var vm = this
        axios.get('https://steemflow-exch-api.herokuapp.com/' + vm.direction + '/' + vm.accountname)
          .then(function (response) {
            vm.results = response.data.exch
            vm.loading = false
          })
      }
    },
  }
</script>

<style scoped>
  #btext {
    color: rgb(41.2%, 41.2%, 41.2%);
  }

  h1 {
    color: rgb(42.1%, 37.3%, 37.3%);
    font-family: 'Luckiest Guy', cursive;
  }

  h4 {
    color: rgb(42.1%, 37.3%, 37.3%);
    font-family: 'Luckiest Guy', cursive;
  }

  .jumbotron {
    margin-top: 8%;

    background: white;
  }

  .fa-spinner {
    color: rgb(87.8%, 35.9%, 35.9%);
  }

  .btn:hover {
    background: rgb(87.8%, 35.9%, 35.9%);
  }
</style>