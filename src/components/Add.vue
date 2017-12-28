<template>
  <div class="add container">
    <h3 class="page-header">Add customer</h3>
    <form @submit.prevent="addCustomer">
    	<div class="well">
            <h4>Customer Info</h4>
            <div class="form-group">
                <label>First Name</label>
                <input type="text" class="form-control" placeholder="First Name" v-model="customer.first_name">
            </div>
            <div class="form-group">
                <label>Last Name</label>
                <input type="text" class="form-control" placeholder="Last Name" v-model="customer.last_name">
            </div>
        </div>
        <div class="well">
            <h4>Customer Contact</h4>
            <div class="form-group">
                <label>Email</label>
                <input type="text" class="form-control" placeholder="Email" v-model="customer.email">
            </div>
            <div class="form-group">
                <label>Phone</label>
                <input type="text" class="form-control" placeholder="Phone" v-model="customer.phone">
            </div>
        </div>

        <div class="well">
            <h4>Customer Location</h4>
            <div class="form-group">
                <label>Address</label>
                <input type="text" class="form-control" placeholder="Address" v-model="customer.address">
            </div>
            <div class="form-group">
                <label>City</label>
                <input type="text" class="form-control" placeholder="City" v-model="customer.city">
            </div>
            <div class="form-group">
                <label>State</label>
                <input type="text" class="form-control" placeholder="State" v-model="customer.state">
            </div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
    	customer: {}
    }
  },
  methods: {
  	addCustomer(e){
  		// validation
		if(!this.customer.first_name || !this.customer.last_name || !this.customer.email){
			console.log("Please fill in all the required fields");
		}
		else{
			// capture all customer info from form
			let newCustomer = {
				first_name: this.customer.first_name,
				last_name: this.customer.last_name,
				phone: this.customer.phone,
				email: this.customer.email,
				address: this.customer.address,
				city: this.customer.city,
				state: this.customer.state
			}
			
			// POST new customer to the API endpoint
			this.$http.post('http://localhost:8080/api/customers/add', newCustomer)
				.then(function(response){
					// redirect to home page
					this.$router.push({path: '/', query: {alert: "Customer Added"}});
				});
		}
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
