# Telemora

---

## About Us

We build innovative decentralized applications that integrate the **TON blockchain** with **Telegram Mini Apps (TMAs)**. Our focus is on creating mixed on-chain and off-chain platforms, such as multivendor marketplaces, enabling secure and transparent transactions using **TON cryptocurrency**.

---

## Our Flagship Project: Mixed Multivendor Marketplace Telegram Mini App

Our primary project is a comprehensive multivendor marketplace designed as a **Telegram Mini App (TMA)**. This application seamlessly blends **on-chain (blockchain-based)** and **off-chain (server-based)** components to offer a robust and user-friendly experience for buying and selling goods and services using **TON cryptocurrency**.

### Key Features

* **Multivendor Support:** Users can effortlessly set up their own shops and offer products or services.
* **TON Cryptocurrency Integration:** All transactions within the marketplace are powered by the secure and efficient TON cryptocurrency.
* **Hybrid Architecture:** A powerful combination of an off-chain backend for data management and monitoring, and on-chain smart contracts for secure payment processing.
* **Automated Commission System:** Our smart contract automatically deducts a marketplace commission from each transaction, ensuring fair and transparent fee collection.
* **Admin Fund Withdrawal:** A secure mechanism allows the marketplace administrator to withdraw accumulated commissions from the smart contract.

### Technical Deep Dive

#### 1. On-Chain Component: Smart Contract

The core of our marketplace's payment logic resides in a smart contract, meticulously developed in **FunC**.

* **Payment Reception:** The smart contract is engineered to receive **internal messages** containing TON tokens, representing payments from buyers.
* **Commission Deduction:** Upon receiving a payment, the contract autonomously deducts a predefined **commission fee** for the marketplace.
* **Seller Payout:** After the commission is deducted, the remaining amount is securely dispatched to the respective seller's wallet address via **internal outbound messages**.
* **Commission Accumulation:** All collected commission fees are systematically accumulated and stored as part of the contract's **persistent data**.
* **Admin Withdrawal Function:** A controlled function is implemented, exclusively permitting the **admin's pre-registered wallet address** to initiate withdrawals of the accumulated commission funds. This function rigorously verifies the source address of the message to ensure it matches the authorized admin wallet.

**Smart Contract Design Considerations:**

* **Transaction Costs:** The contract is designed to account for inherent TON network transaction costs (gas and forwarding fees), ensuring incoming messages include sufficient TON to cover these.
* **Replay Protection:** We leverage the built-in replay protection of TON smart wallets to guarantee secure and idempotent transactions, preventing duplicates.
* **Immutability:** The smart contract's code and data are inherently immutable, ensuring the integrity and reliability of the marketplace's core logic.

#### 2. Off-Chain Component: Backend for Transaction Monitoring

Our off-chain backend system plays a crucial role in monitoring and logging all relevant transactions on the TON blockchain that involve the marketplace's smart contract.

* **Blockchain Interaction:** We utilize **TON HTTP-based APIs** for efficient interaction with indexed blockchain data.
* **Data Indexing:** Tools like **Anton**, an open-source indexer for TON, are employed to access and analyze blockchain data efficiently.
* **Transaction Fetching:** The `getTransactions` method is used to retrieve transactions related to our smart contract. The backend periodically fetches the **latest `last_transaction_id`** using `getAddressInformation`, then loads and filters transactions to ensure the `source` is not empty and the `destination` matches the smart contract's address. To detect new transactions, the `lt` (logical time) of the last processed transaction is stored.
* **Transaction Details:** The backend tracks key transaction data, including the **`source` (payer wallet address), `hash`, `value`, and `comment`**.
* **Database:** A **PostgreSQL** database is used for persistent storage and logging of all monitored transaction data.

#### 3. Payment Flow and Wallet Interaction

Our payment process is designed for security and user-friendliness, powered by **TON Connect**.

* **Payment Initiation:** When a buyer clicks a payment button within the Telegram Mini App, the process begins.
* **Purchase Data Packaging:** The app generates a comprehensive purchase data package, including the smart contract address, the exact TON amount, the relevant Opcode, and any necessary metadata.
* **TON Connect Integration:** This data package is securely transmitted to the user's crypto wallet via **TON Connect**, the standard communication protocol for the TON ecosystem.
* **User Signature & Confirmation:** The user's wallet displays the transaction details for their review and requires their explicit **signature and confirmation**.
* **Transaction Submission:** Upon user confirmation, the signed transaction is submitted directly from the user's wallet to the marketplace's smart contract on the TON blockchain.
* **Modern Wallet Integration:** We exclusively use **TON Connect** for wallet interaction, deprecating older methods like `ton://` links due to their security limitations.

### Tools and Technologies

* **Telegram Mini App (TMA) Development:**
    * **Next.js:** For building the reactive and user-friendly front-end of the web application.
    * **`@telegram-apps/sdk-react`:** For seamless integration with Telegram Mini App functionalities and an enhanced user experience.
* **TON Blockchain Interaction:**
    * **TypeScript SDKs:** For robust interaction with the TON blockchain from both the off-chain backend and potentially the TMA.
* **Smart Contract Development:**
    * **FunC:** The specialized programming language for crafting secure and efficient TON smart contracts.
* **Telegram Bots & Backend:**
    * **NestJS:** For developing the scalable Telegram bot and the backend system responsible for interacting with the TON Center API and managing user/transaction data.
    * **PostgreSQL:** For reliable and persistent storage of user and transaction data.

---

## Get Involved

We are passionate about building the future of decentralized applications on TON. If you're interested in contributing or learning more about our projects, feel free to explore our repositories or reach out to us.

---
