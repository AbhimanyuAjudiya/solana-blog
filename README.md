# Solana Blog

Welcome to the **Solana Blog** project repository! This decentralized application (DApp) leverages blockchain technology to implement an auction platform on the Solana network. Here you can write blogs and tell your story to the world. This project is built using Solana and Anchor.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Smart Contracts](#smart-contracts)
- [Testing](#testing)
- [Frontend](#frontend)
- [Contributing](#contributing)
- [License](#license)

## Overview

The **Solana Blog** provides a user to share there thoughts and ideas to the world. The user can write blogs and publish them on the blockchain. The user can also read blogs written by other users. In future we can add this functionality that the user can also tip the author of the blog if they like the blog, the user can also comment on the blog and interact with other users.

## Features

- **Write Blogs**: The user can write blogs and publish them on the blockchain.
- **Read Blogs**: The user can read blogs written by other users.
- **Tip the Author**: The user can tip the author of the blog if they like the blog.
- **Comment on Blogs**: The user can comment on the blog and interact with other users.
- **Solana Blockchain**: The project is built on the Solana blockchain.
- **Anchor**: The project is built using Anchor.


## Getting Started

Follow these steps to set up the project locally.

### Prerequisites

1. Node.js: Ensure Node.js is installed. Download it from [nodejs.org](https://nodejs.org/).

### Installation

1. Clone the repository:

```bash
  git clone https://github.com/AbhimanyuAjudiya/solana-blog
```

2. Navigate to the project directory:

```bash
  cd solana-blog
```

3. Install required npm packages:

```bash
 npm install
```
4. Install [Anchor](https://www.anchor-lang.com/docs/installation)
## Usage

1. Build your project:

```bash
 anchor build
```

2. Make sure that your program ID is updated and run:
    
```bash
 anchor test
```

2. Open your web browser and navigate to `http://localhost:3000` to access the DApp.

3. Connect your Ethereum wallet (e.g., MetaMask) to the DApp.

4. Browse ongoing auctions, place bids, and monitor your auction activity.

## Smart Contracts

The smart contracts in this project facilitate the auction process. They handle bids, auction creation, and winner determination. These contracts are deployed on the Ethereum blockchain.

- `AuctionFactory.sol`: Responsible for creating new auctions.
- `Auction.sol`: Manages bidding and winner determination for individual auctions.

## Testing

Smart contract tests are located in the `test` folder. These tests ensure the correct functioning of the smart contract. To run the tests, follow these steps:

1. Open a terminal in the project directory.
2. Run the following command to execute the tests:

```bash
truffle test
```

This command will initiate the smart contract tests and display the results in the terminal.

![image](https://github.com/Rise-In/XXX-Bootcamp-FinalCase/assets/140731987/8dc52183-626c-4f39-9408-a37ba496a345)

## Frontend

The DApp frontend is built using modern web technologies including React.js. It provides an intuitive and interactive user interface for auction participation.

- **React.js**: Powers the DApp's user interface.
- **Web3.js**: The Ethereum JavaScript API for smart contract interaction.
- **MetaMask**: A popular Ethereum wallet browser extension for secure transactions.

## Contributing

Contributions to this project are welcome! To contribute:

1. Fork the repository.
2. Create a new branch for your feature/bug fix.
3. Make changes and test thoroughly.
4. Commit with clear and concise messages.
5. Push changes to your fork.
6. Submit a pull request describing your changes.

## License

This project is licensed under the [MIT License](LICENSE).

---

Thank you for your interest in the Web3 Auction DApp project! For questions or suggestions, reach out to us or open an issue on [GitHub](https://github.com/Rise-In/XXX-Bootcamp-FinalCase). Happy bidding on the blockchain! 🚀