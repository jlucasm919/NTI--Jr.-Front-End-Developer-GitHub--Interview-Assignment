<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mortgage Repayment Calculator</title>
    <!-- Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <!-- Custom CSS -->
    <style>
        /* Custom styling can go here, but minimize usage */
    </style>
</head>
<body>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-6 offset-md-3">
                <form id="mortgageForm">
                    <div class="form-group">
                        <label for="loanAmount">Loan Amount ($)</label>
                        <input type="number" class="form-control" id="loanAmount" name="loanAmount" required>
                        <div class="invalid-feedback">
                            Please enter a valid loan amount.
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="interestRate">Interest Rate (%)</label>
                        <input type="number" step="0.01" class="form-control" id="interestRate" name="interestRate" required>
                        <div class="invalid-feedback">
                            Please enter a valid interest rate.
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="loanTerm">Loan Term (years)</label>
                        <input type="number" class="form-control" id="loanTerm" name="loanTerm" required>
                        <div class="invalid-feedback">
                            Please enter a valid loan term.
                        </div>
                    </div>
                    <button type="submit" class="btn btn-primary btn-block">Calculate</button>
                </form>
                <div class="mt-4">
                    <h4>Repayment Details</h4>
                    <p>Monthly Repayment: <span id="monthlyRepayment">$0.00</span></p>
                    <p>Total Repayment: <span id="totalRepayment">$0.00</span></p>
                </div>
            </div>
        </div>
    </div>

    <!-- Bootstrap JS and dependencies -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@1.16.1/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    
    <script>
        document.getElementById('mortgageForm').addEventListener('submit', function(event) {
            event.preventDefault();

            // Fetch input values
            let loanAmount = parseFloat(document.getElementById('loanAmount').value);
            let interestRate = parseFloat(document.getElementById('interestRate').value);
            let loanTerm = parseInt(document.getElementById('loanTerm').value);

            // Check if inputs are valid numbers
            if (isNaN(loanAmount) || isNaN(interestRate) || isNaN(loanTerm) || loanAmount <= 0 || interestRate <= 0 || loanTerm <= 0) {
                // Show validation messages
                if (isNaN(loanAmount) || loanAmount <= 0) {
                    document.getElementById('loanAmount').classList.add('is-invalid');
                } else {
                    document.getElementById('loanAmount').classList.remove('is-invalid');
                }
                if (isNaN(interestRate) || interestRate <= 0) {
                    document.getElementById('interestRate').classList.add('is-invalid');
                } else {
                    document.getElementById('interestRate').classList.remove('is-invalid');
                }
                if (isNaN(loanTerm) || loanTerm <= 0) {
                    document.getElementById('loanTerm').classList.add('is-invalid');
                } else {
                    document.getElementById('loanTerm').classList.remove('is-invalid');
                }
                return;
            }

            // Calculate monthly and total repayments
            let monthlyInterest = (interestRate / 100) / 12;
            let numberOfPayments = loanTerm * 12;
            let monthlyRepayment = (loanAmount * monthlyInterest) / (1 - Math.pow(1 + monthlyInterest, -numberOfPayments));
            let totalRepayment = monthlyRepayment * numberOfPayments;

            // Display results
            document.getElementById('monthlyRepayment').textContent = '$' + monthlyRepayment.toFixed(2);
            document.getElementById('totalRepayment').textContent = '$' + totalRepayment.toFixed(2);
        });
    </script>
</body>
</html>

