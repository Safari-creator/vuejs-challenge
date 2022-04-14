<template>
	<div class="container">
		<div class="accountDetails mb-4">
			<h3>
				Account No: <b>{{ this.account }}</b>
			</h3>
			<div class="d-flex justify-content-between">
				<h4>Available balance: <b>123 </b></h4>
				<h4>Status: <span class="text-success"> Active </span></h4>
			</div>
		</div>
		<h3>Transactions</h3>
		<div class="table table-hover table-striped mb-5">
			<thead>
				<th>No</th>
				<th>Transaction Date</th>
				<th>Amount</th>
				<th>Type</th>
				<th>Description</th>
				<th>Business Date</th>
				<th>Merchant Name</th>
				<th>Merchant Id</th>
				<th>Balance</th>
			</thead>
			<tbody>
				<tr v-for="(item, index) in transactions" :key="item">
					<td>{{ index + 1 }}</td>
					<td>{{ getFormatedDate(item.TransactionDate, "DD-MM-yyyy") }}</td>
					<td>{{ item.Amount }}</td>
					<td>{{ item.TransactionTypeId }}</td>
					<td>{{ item.Description }}</td>
					<td>{{ getFormatedDate(item.BusinessDate, "DD-MM-yyyy") }}</td>
					<td>{{ item.MerchantName }}</td>
					<td>{{ item.MerchantId }}</td>
					<td>{{ item.AvailableBalance }}</td>
				</tr>
			</tbody>
		</div>

		<h3>Unsettled Transactions</h3>
		<div class="table table-hover table-striped">
			<thead>
				<th>No</th>
				<th>Transaction Date</th>
				<th>Amount</th>
				<th>Type</th>
				<th>Description</th>
				<th>Business Date</th>
				<th>Merchant Name</th>
				<th>Merchant Id</th>
				<th>Balance</th>
			</thead>
			<tbody>
				<tr v-for="(item, index) in unsettledTransactions" :key="item">
					<td>{{ index + 1 }}</td>
					<td>{{ getFormatedDate(item.TransactionDate, "DD-MM-yyyy") }}</td>
					<td>{{ item.Amount }}</td>
					<td>{{ item.TransactionTypeId }}</td>
					<td>{{ item.Description }}</td>
					<td>{{ getFormatedDate(item.BusinessDate, "DD-MM-yyyy") }}</td>
					<td>{{ item.MerchantName }}</td>
					<td>{{ item.MerchantId }}</td>
					<td>{{ item.AvailableBalance }}</td>
				</tr>
			</tbody>
		</div>
	</div>
</template>

<script>
import moment from "moment";

export default {
	name: "Transactions",

	data() {
		return {
			transactions: [],
			unsettledTransactions: [],
			account: "",
		};
	},

	created() {
		console.log(this.$store.state.transactionDetails);

		this.transactions = this.$store.state.transactionDetails.Statement.Transactions;

		this.unsettledTransactions = this.$store.state.transactionDetails.Statement.NotSettled;

		this.account = this.transactions[0].AccountNumber;

	},

	methods: {
		getFormatedDate(date, format) {
			return moment(date).format(format);
		},
	},
};
</script>



<style scoped>
.accountDetails {
	border-bottom: 1px solid gray;
}
</style>
