### HTML and CSS Code

The HTML and CSS code creates a simple web page for accepting USDT payments. The page includes a form where users can enter the amount of USDT they want to send and displays a fixed USDT wallet address. It also includes buttons to copy the wallet address and check the balance using web3.js.

### HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>USDT Payment Page</title>
    <style>
        /* CSS styles for the page */
    </style>
    <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
</head>
<body>
    <div class="container">
        <h1>Pay with USDT</h1>
        <form id="payment-form">
            <label for="amount">Amount (USDT):</label>
            <input type="number" id="amount" name="amount" required>
            <label for="address">USDT Wallet Address:</label>
            <input type="text" id="address" name="address" value="YOUR_USDT_WALLET_ADDRESS" readonly>
            <button type="button" onclick="copyAddress()">Copy Wallet Address</button>
            <button type="button" onclick="checkBalance()">Check Balance</button>
        </form>
        <div id="balance-result"></div>
    </div>

    <script>
        /* JavaScript functions for copying the address and checking the balance */
    </script>
</body>
</html>
```

### CSS Styles

The CSS styles are used to improve the appearance of the page. It centers the content, adds padding, and styles the form elements and buttons.

### JavaScript Functions

1. **Copy Address Function**: This function copies the USDT wallet address to the clipboard when the "Copy Wallet Address" button is clicked.

```javascript
function copyAddress() {
    const address = document.getElementById('address');
    address.select();
    address.setSelectionRange(0, 99999); // For mobile devices

    navigator.clipboard.writeText(address.value).then(() => {
        alert('Wallet address copied to clipboard');
    }).catch(err => {
        alert('Failed to copy address: ', err);
    });
}
```

2. **Check Balance Function**: This function uses web3.js to check the balance of the USDT wallet address. It connects to the Ethereum network via Infura, interacts with the USDT contract, and retrieves the balance.

```javascript
async function checkBalance() {
    const address = document.getElementById('address').value;
    const web3 = new Web3('https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID'); // Replace with your Infura Project ID
    const contractAddress = '0xdac17f958d2ee523a2206206994597c13d831ec7'; // USDT contract address
    const minABI = [
        // Only the balanceOf function from the ABI
        {
            "constant": true,
            "inputs": [{"name": "_owner", "type": "address"}],
            "name": "balanceOf",
            "outputs": [{"name": "balance", "type": "uint256"}],
            "type": "function"
        }
    ];

    const contract = new web3.eth.Contract(minABI, contractAddress);
    try {
        const balance = await contract.methods.balanceOf(address).call();
        const usdtBalance = web3.utils.fromWei(balance, 'mwei'); // Convert balance from wei to USDT
        document.getElementById('balance-result').innerText = `Current Balance: ${usdtBalance} USDT`;
    } catch (error) {
        alert('Failed to fetch balance: ', error);
    }
}
```

### Notes:
- **Replace `YOUR_USDT_WALLET_ADDRESS`**: Make sure to replace this text with your actual USDT wallet address.
- **Replace `YOUR_INFURA_PROJECT_ID`**: Make sure to replace this text with your Infura Project ID.
- **Balance Conversion**: The code converts the balance from wei to USDT using `web3.utils.fromWei`.
  ## Contact
  avrmicrotech@gmail.com
 
