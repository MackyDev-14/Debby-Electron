<template>
	<v-container fluid pa-3>

		<v-card 
			color="blue-grey darken-2"
			class="white--text debtors"
		>
			<v-card-title primary-title>
			   <div class="headline">{{debtData.name}}</div>
			   <v-spacer></v-spacer>
			   <v-card-actions>
			   		Total Debt: {{debtData.debt}} php
			   </v-card-actions>
			</v-card-title>
		</v-card>

		<div id = "table-con">
			<div v-for = "debts in debtData.debts" class = "table">
				<v-layout row wrap>
					<p>{{debts.date}}</p>
					<v-spacer></v-spacer>
					<p>Total Credit: {{debts.totalCredits}}</p>
				</v-layout>
				<v-data-table
				    :headers="headers"
				    :items="debts.items"
				    class="elevation-1"
				    hide-actions
				  >
				    <template v-slot:items="props">
				      <td>{{ props.item.name }}</td>
				      <td class="text-xs-left">{{ props.item.price }}</td>
				    </template>
				</v-data-table>
				<v-btn>Paid</v-btn>
			</div>
		</div>

		<DebbieForm @addDebt="addDebt" />

	</v-container>
</template>


<script>
	import DebbieForm from "./DebbieForm"

	export default{
		name: "ViewDebt",
		components: {
			DebbieForm
		},
		props: ["debtData"],
		created(){
		},
		data(){
			return{
				headers: [
		          {
		            text: 'Item Name',
		            align: 'left',
		            sortable: false,
		            value: 'name'
		          },
		          { text: 'Price', value: 'price', sortable: false,},
		        ],
			}
		},
		methods: {
			addDebt(  totalCredits, newDebt){
				this.debtData.debt = this.debtData.debt + totalCredits;
				this.debtData.debts.push(newDebt)
			}
		}
	}
</script>

<style scoped>
	.table{
		margin-bottom: 80px;
	}
	#table-con{
		max-height: 78vh;
		height: 78vh;
		overflow-y: scroll;
		padding: 40px;
	}
</style>