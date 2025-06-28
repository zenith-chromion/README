# 🔱 ZenithVault – LP-Governed Cross-Chain Fund Management Protocol

## 🌐 Overview

**ZenithVault** is a cross-chain DeFi protocol where **skilled fund managers** can create strategy-based liquidity pools, and **crypto holders (LPs)** can passively earn yields by providing liquidity. LPs receive ERC-20 tokens that also serve as **voting power** in DAO decisions. With vaults deployed across **Ethereum Sepolia**, **Arbitrum Sepolia**, and **Base Sepolia**, and using **Chainlink CCIP**, ZenithVault enables decentralized governance and secure, isolated liquidity pools across chains.

---

## 🎯 Key Highlights

- 🧑‍💼 **Fund Managers (FMs)** launch strategy-based vaults and earn royalties on profit
- 💰 **Liquidity Providers (LPs)** stake assets, receive ERC-20 LP tokens, and govern vaults
- 🗳️ **DAO Voting via LP Tokens**: No governance token — voting power = LP token balance
- 🌐 **Multi-Chain Architecture**: Ethereum, Arbitrum, and Base testnets supported
- 🔗 **Chainlink CCIP Integration**: DAO proposals sync across chains
- 🏗️ **Factory + PoolManager**: Automated vault deployment and management

---

## 🧩 Smart Contract Structure

| Contract             | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `pool.sol`           | Logic for vaults: deposits, withdrawals, LP token minting                   |
| `poolManager.sol`    | Registry for managing fund managers and vault configs                       |
| `dao.sol`            | DAO contract governed by LP token holders                                   |
| `daoAggregator.sol`  | Aggregates DAO decisions and pushes updates cross-chain                     |
| `factory.sol`        | Deploys new pool contracts with preconfigured strategies                    |
| `ccipSender.sol`     | Encodes and sends governance messages to other chains via Chainlink CCIP    |
| `deployer.sol`       | Utility for initializing contract infrastructure                            |

---

## 🧠 Voting Logic

ZenithVault uses **LP token-weighted voting** for DAO governance.  
No separate governance token exists.

- 💼 LPs receive LP tokens when depositing into pools
- 🗳 Voting power = LP token balance at snapshot block
- 📦 Votes can:
  - Add/remove fund managers
  - Change FM tier
  - Update royalty % per tier
  - Change withdrawal caps for FMs

---

## 🗳 DAO Proposal Types

| Proposal Type                        | Description                                                    |
|-------------------------------------|----------------------------------------------------------------|
| Add Fund Manager                    | Approves a new FM with initial tier                            |
| Remove Fund Manager                 | Revokes FM’s vault access and control                          |
| Change FM Tier                      | Updates FM's performance tier (affects royalties, withdrawal %)|
| Change Tier Royalty %               | Sets new royalty % for specific tier                           |
| Change Tier Withdrawal Limit %      | Updates how much liquidity each tier can withdraw              |

> ✅ Once approved, these proposals are propagated cross-chain via `daoAggregator` + `ccipSender`.

---

## 🛠 Development Environment

### ✅ Networks

| Chain             | Role                       | Chain ID |
|------------------|----------------------------|----------|
| Ethereum Sepolia | DAO & primary control hub  | 11155111 |
| Arbitrum Sepolia | FM & LP vault deployment    | 421614   |
| Base Sepolia     | Additional vault hosting    | 84532    |

