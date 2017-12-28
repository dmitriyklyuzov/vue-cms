<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h3 class="page-header">Manage customers</h3>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Email</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in customers">
          <td>{{customer.first_name}}</td>
          <td>{{customer.last_name}}</td>
          <td>{{customer.email}}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert';
  export default {
    name: 'customers',
    data () {
      return {
        customers: [],
        alert: ''
      }
    },
    methods: {
      fetchCustomers(){
        this.$http.get('http://localhost:8080/api/customers')
          .then(function(response){
            this.customers = response.body;
          });
      }
    },
    // fetch customers on create
    created: function(){
      // if there is an alert msg sent over with the redirect
      if(this.$route.query.alert){
        // set this alert to the alert msg
        this.alert = this.$route.query.alert;
      }
      this.fetchCustomers();
    },
    // fetch customers on update
    updated: function(){
      this.fetchCustomers();
    },
    components: {
      Alert
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
