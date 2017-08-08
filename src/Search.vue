<template>
  <div v-if="results.length > 0">
    <p id="nresult"> {{ results.length }} results found</p>
     <table class="table table-hover">
      <thead>
        <tr>
         <th> From </th>
         <th> To </th>
         <th> Ammount </th>
         <th> Asset </th>
         <th> Timestamp </th>
         </tr>
      </thead>
      <tbody>
        <tr v-for="result in results">
          <td> {{result.from}}</td>
          <td> {{result.to}}</td>
          <td> {{result.amount.amount}}</td>
          <td> {{result.amount.asset}}</td>
          <td> {{result.timestamp}}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
    props: ['results'],
    data: function() {
      return {
        
      }
    },
 }
</script>

<style scoped>
 #nresult {
   color: rgb(95.6%, 29.8%, 36.3%);
 }

.table-hover tbody tr:hover td, .table-hover tbody tr:hover th {
   background-color: rgba(220, 0, 0, 0.2);
}

p, th, td {
   font-family: 'Raleway', sans-serif;
}

.table th{
   text-align: center;   
}

.table td{
   text-align: center;   
}

</style>