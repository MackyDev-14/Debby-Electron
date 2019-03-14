<template>
	<div id = "add-debt">
		<v-dialog
		   	v-model="dialog"
		      width="500"

			>
		      <template v-slot:activator="{ on }">
		        <v-btn
		          color="red lighten-2"
		          dark
		          v-on="on"
		          @click = "setDate"
		        >
		          Add new Debt
		        </v-btn>
		      </template>

		      <v-card>
		        <v-card-title
		          class="headline grey lighten-2"
		          primary-title
		        >
		          Add new Debt
		        </v-card-title>

		        <v-card-actions>
		          <v-card-text>
		            {{debt.date}}
		          </v-card-text>
		          <v-card-text>
		            Total Credits: {{debt.totalCredits}} Php
		          </v-card-text>
		        </v-card-actions>

		        <v-card-actions>
		        	<v-text-field
			            label="Item name"
			            v-model ="itemName" class = "mx-3"
			        >
			        </v-text-field>

			        <v-text-field
			            label="Price"
			            v-model ="price" class = "mr-3"
			        >
			        </v-text-field>

			        <v-btn @click = "addItem" class = "mr-3">Add</v-btn>
		        </v-card-actions>

			        <v-data-table
					    :headers="headers"
					    :items="debt.items"
					    class="elevation-1 ma-2 table"
					    hide-actions
					  >
					    <template v-slot:items="props">
					      <td>{{ props.item.name }}</td>
					      <td class="text-xs-left">{{ props.item.price }}</td>
					    </template>
					</v-data-table>

		        <v-divider></v-divider>

		        <v-card-actions>
			        <v-btn
			            color="danger"
			            flat
			            @click = "reset"
			        >
		            Reset
		          </v-btn>
		          <v-spacer></v-spacer>
		          <v-btn
		            color="primary"
		            flat
		            @click = "addDebt"
		          >
		            Add Debt
		          </v-btn>
		        </v-card-actions>
		      </v-card>

    		</v-dialog>
    	</div>
</template>

<script>
	export default{
		name: "DebbieForm",
		data(){
			return{
			itemName: null,
			price: null,
			dialog: false,
			headers: [
		          {
		            text: 'Item Name',
		            align: 'left',
		            sortable: false,
		            value: 'name'
		          },
		          { text: 'Price', value: 'price', sortable: false,},
		        ],
			debt: {date: null,totalCredits: 0, items: []}
			}
		},
		methods: {
			addItem(){
				var totalCredits = this.debt.totalCredits + Number(this.price);
				this.debt.totalCredits = totalCredits;
				this.debt.items.push({name: this.itemName, price: this.price});
				this.itemName = null;
				this.price = null;
			},
			setDate(){
				this.debt.date = new Date().toLocaleDateString();
			},
			reset(){
				this.debt = {...this.debt, totalCredits: 0, items: []};
			},
			addDebt(){

				this.$emit('addDebt', this.debt.totalCredits , this.debt);
				this.debt = {date: null, totalCredits: 0, items: []};
				this.dialog = false;
			}
		}
	}
</script>

<style scoped>
	.table{
		max-height: 250px;
		height: 250px;
		overflow-y: scroll;
	}
	#add-debt{
		position: absolute;
		bottom: 0;
		right: 0;
		margin-bottom: 52px;
		margin-right: 52px;
	}
</style>