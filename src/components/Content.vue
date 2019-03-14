<template>
	<v-container fluid pa-3 id = "container">

			<input
				placeholder="Enter name here. . ."
				id = "name-input"
			>
	 	  	<div id = "debbies">
		 	  	<v-card 
		 	  		v-for = "debtor in debtors"
		 	  		color="blue-grey darken-2"
		 	  		class="white--text debtors"
		 	  	>
	              <v-card-title primary-title>
	                 <div class="headline">{{debtor.name}}</div>
	                 <v-spacer></v-spacer>
	      			<v-card-actions>
	      			   Total Debt: {{debtor.debt}} php
	      			</v-card-actions>
	      			 <v-btn @click="$emit('viewDebt', debtor)" >View</v-btn>
	                 <v-btn>Paid</v-btn>
	              </v-card-title>
		 	  	</v-card>
	 	  	</div>
	 	<div id = "add-debtor">

	 		<v-dialog
		      v-model="dialog"
		      width="500"
			>
		      <template v-slot:activator="{ on }">
		        <v-btn
		          color="red lighten-2"
		          dark
		          v-on="on"
		        >
		          Add new Debtor
		        </v-btn>
		      </template>

		      <v-card>
		        <v-card-title
		          class="headline grey lighten-2"
		          primary-title
		        >
		          Add new Debtor
		        </v-card-title>

		        <v-card-actions>
		        	<v-text-field
			            label="New Debtor"
			            placeholder="Enter name"
			            v-model ="newDebtor"
			        >
			        </v-text-field>
		        </v-card-actions>

		        <v-divider></v-divider>

		        <v-card-actions>
		          <v-spacer></v-spacer>
		          <v-btn
		            color="primary"
		            flat
		            @click = "addNewDebtor"
		          >
		            Add Debtor
		          </v-btn>
		        </v-card-actions>
		      </v-card>

    		</v-dialog>
	 	 </div>
	</v-container>
</template>

<script>
	export default{
		name: "Content",
		props: ["debtors"],
		data(){
			return{
				dialog: false,
				newDebtor: null,
			}
		},
		methods: {
			addNewDebtor(){
				this.$emit('addNewDebtor', {name: this.newDebtor,debt:0, debts: []})
				this.newDebtor = null
				this.dialog = false
			}
		}
	}
</script>

<style scoped>
	#container{
		flex: 1;
		height: 100vh;
		flex-direction: column;
	}
	#name-input{
		box-sizing: border-box;
		padding: 4px;
		width: 50%;
		height: 48px;
		border-bottom: 2px solid black;
		font-size: 24px;
		margin-bottom: 30px;
	}
	#name-input:focus{
		outline: none;
	}
	#debbies{
		overflow-y: scroll;
		max-height: 78vh; 
	}
	#add-debtor{
		position: absolute;
		bottom: 0;
		right: 0;
		margin-bottom: 52px;
		margin-right: 52px;
	}
	.debtors{
		margin-bottom: 10px;
	}
</style>