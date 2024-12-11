<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Dubai Jackpot - Play, Win, and Enjoy!">
    <title>Dubai Jackpot</title>
    <style>
        /* General Styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 0;
        }
        h1, h2, h3 {
            margin: 0;
        }
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            text-align: center;
        }
        header {
            background-color: #ff5722;
            color: white;
            padding: 15px 0;
        }
        nav a {
            margin: 0 15px;
            color: white;
            text-decoration: none;
            font-weight: bold;
        }
        .section {
            padding: 50px 0;
        }
        .btn {
            background-color: #ff5722;
            color: white;
            padding: 10px 20px;
            text-decoration: none;
            border: none;
            cursor: pointer;
            font-size: 1em;
            border-radius: 5px;
        }
        .btn:hover {
            background-color: #e64a19;
        }
        .auth-form {
            display: flex;
            flex-direction: column;
            max-width: 300px;
            margin: 20px auto;
        }
        .auth-form input {
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .auth-form button {
            background-color: #ff5722;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .auth-form button:hover {
            background-color: #e64a19;
        }
        #gameSection {
            display: none;
        }
        #ticketDisplay, #resultDisplay {
            margin-top: 20px;
            font-size: 1.5em;
            font-weight: bold;
            color: #ff5722;
        }
        #balanceDisplay, #withdrawDisplay {
            margin-top: 20px;
            font-size: 1.2em;
            color: #333;
        }
        /* Responsive Design */
        @media (max-width: 768px) {
            .container {
                width: 95%;
            }
            nav a {
                margin: 0 10px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <h1>Dubai Jackpot</h1>
            <nav>
                <a href="#signup">Sign Up</a>
                <a href="#login">Login</a>
                <a href="#gameSection">Play Lottery</a>
                <a href="#about">About</a>
                <a href="#contact">Contact</a>
            </nav>
        </div>
    </header>

    <!-- Sign-Up Section -->
    <section id="signup" class="section">
        <div class="container">
            <h2>Sign Up</h2>
            <form class="auth-form" id="signupForm">
                <input type="text" id="signupUsername" placeholder="Username" required>
                <input type="password" id="signupPassword" placeholder="Password" required>
                <input type="email" id="signupEmail" placeholder="Email" required>
                <input type="text" id="signupReferralCode" placeholder="Referral Code (Optional)">
                <button type="submit">Sign Up</button>
            </form>
            <p id="signupMessage"></p>
        </div>
    </section>

    <!-- Login Section -->
    <section id="login" class="section">
        <div class="container">
            <h2>Login</h2>
            <form class="auth-form" id="loginForm">
                <input type="text" id="loginUsername" placeholder="Username" required>
                <input type="password" id="loginPassword" placeholder="Password" required>
                <button type="submit">Login</button>
            </form>
            <p id="loginMessage"></p>
        </div>
    </section>

    <!-- Lottery Game Section -->
    <section id="gameSection" class="section">
        <div class="container">
            <h2>Welcome to Dubai Jackpot!</h2>
            <button class="btn" id="generateTicketBtn">Generate Lottery Ticket</button>
            <div id="ticketDisplay"></div>
            <button class="btn" id="checkResultBtn">Check Result</button>
            <div id="resultDisplay"></div>
            <button class="btn" id="historyBtn">View Ticket History</button>
            <div id="historyDisplay"></div>
        </div>
    </section>

    <!-- Balance and Withdraw Section -->
    <section id="balanceSection" class="section">
        <div class="container">
            <h2>Your Balance: ₹<span id="balanceAmount">0</span></h2>
            <button class="btn" id="withdrawBtn">Withdraw</button>
            <div id="withdrawSection" style="display:none;">
                <input type="number" id="withdrawAmount" placeholder="Enter amount to withdraw" min="200" max="50000">
                <button class="btn" id="confirmWithdrawBtn">Confirm Withdrawal</button>
                <p id="withdrawMessage"></p>
            </div>
        </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section">
        <div class="container">
            <h2>About Dubai Jackpot</h2>
            <p>Dubai Jackpot एक रोमांचक गेम है जिसमें आप अपनी किस्मत आजमा सकते हैं और शानदार पुरस्कार जीत सकते हैं। सुरक्षित और पारदर्शी लॉटरी सिस्टम के साथ खेलें।</p>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section">
        <div class="container">
            <h2>Contact Us</h2>
            <p>Email: support@dubaijackpot.com</p>
            <p>Phone: +971 123 4567</p>
        </div>
    </section>

    <!-- JavaScript -->
    <script>
        let balance = 0; // Starting balance
        const ticketHistory = [];
        let currentUser = null; // Track logged-in user

        // Async function for sign-up
        async function signUp(username, password, email, referralCode) {
            // Simulating password hashing (use actual hash in production)
            const hashedPassword = btoa(password); // Simple base64 encoding for demonstration
            return { username, password: hashedPassword, email, referralCode, balance: 0 };
        }

        // Sign-Up Functionality
        document.getElementById('signupForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const username = document.getElementById('signupUsername').value;
            const password = document.getElementById('signupPassword').value;
            const email = document.getElementById('signupEmail').value;
            const referralCode = document.getElementById('signupReferralCode').value;

            // Check if user exists
            if (localStorage.getItem(username)) {
                document.getElementById('signupMessage').textContent = 'User already exists!';
            } else {
                const newUser = await signUp(username, password, email, referralCode);
                localStorage.setItem(username, JSON.stringify(newUser));
                document.getElementById('signupMessage').textContent = 'Sign-up successful!';
                document.getElementById('signupForm').reset();
            }
        });

        // Login Functionality
        document.getElementById('loginForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;

            let user = localStorage.getItem(username);
            if (user && JSON.parse(user).password === btoa(password)) { // Simple check (use real hashing in production)
                document.getElementById('loginMessage').textContent = 'Login successful!';
                document.getElementById('gameSection').style.display = 'block';
                document.getElementById('login').style.display = 'none';
                currentUser = JSON.parse(user);
                balance = currentUser.balance;
                document.getElementById('balanceAmount').textContent = balance;
            } else {
                document.getElementById('loginMessage').textContent = 'Invalid credentials!';
            }
        });

        // Withdraw Functionality
        document.getElementById('withdrawBtn').addEventListener('click', () => {
            document.getElementById('withdrawSection').style.display = 'block';
        });

        document.getElementById('confirmWithdrawBtn').addEventListener('click', () => {
            const withdrawAmount = parseInt(document.getElementById('withdrawAmount').value);
            if (withdrawAmount >= 200 && withdrawAmount <= 50000 && withdrawAmount <= balance) {
                balance -= withdrawAmount;
                document.getElementById('balanceAmount').textContent = balance;
                document.getElementById('withdrawMessage').textContent = Withdrawal of ₹${withdrawAmount} successful!;
            } else if (withdrawAmount > 50000) {
                document.getElementById('withdrawMessage').textContent = 'Maximum withdrawal limit is ₹50,000!';
            } else if (withdrawAmount < 200) {
                document.getElementById('withdrawMessage').textContent = 'Minimum withdrawal amount is ₹200!';
            } else {
                document.getElementById('withdrawMessage').textContent = 'Insufficient balance!';
            }
        });
    </script>
</body>
</html>
