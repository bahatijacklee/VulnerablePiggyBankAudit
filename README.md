# 🧠 VulnerablePiggyBankAudit

A smart contract security audit and exploit demonstration for an intentionally vulnerable Ethereum contract named `VulnerablePiggyBank`.

This project includes:
- ✅ The original vulnerable contract
- 🛡️ A fixed, secure version
- 💣 A reentrancy attack contract demonstrating how to exploit the vulnerability

---

## 📂 Project Structure

```

VulnerablePiggyBankAudit/
│
├── contracts/
│   ├── VulnerablePiggyBank.sol      # Original vulnerable contract
│   ├── SafePiggyBank.sol            # Secured version with fixes
│   └── ReentrancyAttack.sol         # Attacker contract to exploit the vulnerability
├── README.md                        # This file

```

---

## 🔍 Audit Summary

### 🔴 Vulnerabilities in `VulnerablePiggyBank.sol`

| Issue                  | Description |
|------------------------|-------------|
| ❌ No access control   | Any address can call `withdraw()` |
| ❌ Reentrancy risk     | Sends Ether before updating state |
| ❌ Unrestricted fallback behavior | Reentrancy becomes possible |
| ❌ Insecure transfer   | Uses `transfer` instead of `call` |
| ❌ Missing visibility  | `constructor()` lacks visibility specifier |

---

## ✅ Fixed Contract: `SafePiggyBank.sol`

### Security Fixes

- ✅ Only owner can withdraw
- ✅ Uses `call` with `require` to prevent failures
- ✅ Follows Checks-Effects-Interactions pattern
- ✅ Eliminates reentrancy risk
- ✅ Declares all visibility explicitly
- ✅ Uses `receive()` for Ether deposits

---

## 💣 Reentrancy Attack Demo: `ReentrancyAttack.sol`

### How It Works

1. The attacker contract deposits ETH into `VulnerablePiggyBank`
2. Calls `withdraw()`, triggering a `receive()` fallback
3. Fallback re-enters `withdraw()` before the state is updated
4. Repeats until the balance is drained

---

## 🚀 Deployment & Testing Instructions (Remix)

1. **Deploy** `VulnerablePiggyBank` and fund it with ETH.
2. **Deploy** `ReentrancyAttack` passing the piggy bank’s address.
3. Call `attack()` with some ETH to start reentrancy attack.
4. Observe repeated draining via fallback calls.
5. Use `drain()` to send stolen funds to attacker wallet.

---

## 🧠 Recommendations

- Always use access control (`onlyOwner`) for sensitive functions.
- Use `call{value: amount}` instead of `transfer` or `send`.
- Follow Checks-Effects-Interactions pattern to avoid reentrancy.
- Consider using OpenZeppelin's `ReentrancyGuard` for additional protection.

---

## 📜 License

MIT License


## ✍️ Author

**Bahati Jacklee**  
GitHub: [@bahatijacklee](https://github.com/bahatijacklee)

Feel free to contribute or report additional issues!
