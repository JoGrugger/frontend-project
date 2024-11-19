<script>
	let principal = 0; // Loan Amount
	let interestRate = 0; // Annual Interest Rate (in %)
	let years = 0; // Loan Duration in years
	let monthlyPayment = null;
	let totalPayment = null;

	// Function to calculate mortgage payments
	const calculateMortgage = () => {
		if (principal > 0 && interestRate > 0 && years > 0) {
			const monthlyRate = interestRate / 100 / 12;
			const totalMonths = years * 12;
			monthlyPayment = (principal * monthlyRate) / (1 - Math.pow(1 + monthlyRate, -totalMonths));
			totalPayment = monthlyPayment * totalMonths;
		} else {
			monthlyPayment = null;
			totalPayment = null;
		}
	};

	// Form reset
	const resetForm = () => {
		principal = 0;
		interestRate = 0;
		years = 0;
		monthlyPayment = null;
		totalPayment = null;
	};
</script>

<div class="container">
	<h1>Mortgage Repayment Calculator</h1>
	<form on:submit|preventDefault={calculateMortgage}>
		<label for="principal">Loan Amount ($)</label>
		<input type="number" id="principal" bind:value={principal} min="0" required />

		<label for="interestRate">Annual Interest Rate (%)</label>
		<input type="number" id="interestRate" bind:value={interestRate} min="0" step="0.01" required />

		<label for="years">Loan Duration (Years)</label>
		<input type="number" id="years" bind:value={years} min="1" required />

		<div>
			<button type="submit" class="calculate">Calculate</button>
			<button type="button" class="reset" on:click={resetForm}>Reset</button>
		</div>
	</form>

	{#if monthlyPayment !== null && totalPayment !== null}
		<div class="results">
			<h2>Results</h2>
			<p><strong>Monthly Payment:</strong> ${monthlyPayment.toFixed(2)}</p>
			<p><strong>Total Repayment:</strong> ${totalPayment.toFixed(2)}</p>
		</div>
	{/if}
</div>

<style>
	/* Simple styles for layout and design */
	.container {
		max-width: 600px;
		margin: 0 auto;
		padding: 2rem;
		font-family: Arial, sans-serif;
	}

	label {
		display: block;
		margin-bottom: 0.5rem;
		font-weight: bold;
	}

	input {
		width: 100%;
		padding: 0.5rem;
		margin-bottom: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
	}

	button {
		padding: 0.75rem 1.5rem;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}

	button.calculate {
		background-color: #007bff;
		color: white;
	}

	button.reset {
		background-color: #dc3545;
		color: white;
		margin-left: 1rem;
	}

	.results {
		margin-top: 2rem;
		padding: 1rem;
		background-color: #f9f9f9;
		border: 1px solid #ddd;
		border-radius: 4px;
	}

	.results p {
		margin: 0.5rem 0;
	}
</style>
