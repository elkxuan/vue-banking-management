<template>
  <div>
    <h1>Admin Dashboard</h1>
    <h2>Summary</h2>

    <!-- Summary Section -->
    <div class="summary">
      <div class="summary-card">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Total Departments</h5>
            <p class="card-text">{{ totalDepartments }}</p>
          </div>
        </div>
      </div>
      <div class="summary-card">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Total Employees</h5>
            <p class="card-text">{{ totalEmployees }}</p>
          </div>
        </div>
      </div>
      <div class="summary-card">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Total Customers</h5>
            <p class="card-text">{{ totalCustomers }}</p>
          </div>
        </div>
      </div>
      <div class="summary-card">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Total Accounts</h5>
            <p class="card-text">{{ totalAccounts }}</p>
          </div>
        </div>
      </div>
      <div class="summary-card">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Total Transactions</h5>
            <p class="card-text">{{ totalTransactions }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Recent Transactions Section -->
    <div class="recent-transactions">
      <h2>Recent Transactions</h2>
      <table class="table table-hover">
        <thead>
          <tr>
            <th>Date</th>
            <th>Description</th>
            <th>Amount</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="transaction in recentTransactions" :key="transaction.id">
            <td>{{ transaction.date }}</td>
            <td>{{ transaction.description }}</td>
            <td>{{ transaction.amount }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      totalDepartments: 10, // Replace with actual data
      totalEmployees: 50, // Replace with actual data
      totalCustomers: 10, // Replace with actual data
      totalAccounts: 10, // Replace with actual data
      totalTransactions: 10, // Replace with actual data
      recentTransactions: [
        { id: 1, date: '2023-09-10', description: 'Payment received', amount: 100 },
        { id: 2, date: '2023-09-09', description: 'Purchase made', amount: -50 },
        // Add more recent transactions
      ],
    };
  },
};
</script>

<style>
/* Add your CSS styling here */
.summary {
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}

.summary-card {
  flex-basis: calc(20% - 20px);
  /* Adjust the width of each summary card */
  margin-right: 50px;
  /* Add some space between the summary cards */
  background-color: #ffffff;
  /* Add a background color */
  padding: 10px;
  /* Add some padding inside the summary card */
}

.card{
  background-color: #ffffff;
  border-radius: 10px;
}
/* Style the card title and card text */
.card-title {
  font-size: 18px;
  margin-bottom: 5px;
  color: #333;
  /* Text color */
}

.card-text {
  font-size: 24px;
  /* Increase font size for the data */
  font-weight: bold;
  /* Make the data text bold */
  color: #0033ff;
  /* Text color for data */
}

.recent-transactions {
  margin-top: 20px;
}
</style>
