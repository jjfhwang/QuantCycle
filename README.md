# QuantCycle: Decentralized, Verifiable, and Privacy-Preserving Crypto Portfolio Management

QuantCycle is a sophisticated, decentralized trading bot built with TypeScript that empowers users to automate and optimize their cryptocurrency portfolios with unparalleled security and transparency. Utilizing smart contract oracles and zero-knowledge succinct non-interactive arguments of knowledge (zk-SNARKs), QuantCycle provides verifiable and privacy-preserving portfolio management strategies on decentralized exchanges (DEXs).

This project aims to address the inherent limitations of traditional centralized trading bots, which often lack transparency and are susceptible to manipulation. QuantCycle leverages the immutability and transparency of blockchain technology to ensure that all trading decisions are executed according to predefined, verifiable rules. The integration of smart contract oracles provides access to reliable and tamper-proof market data, enabling the bot to make informed trading decisions based on real-time price feeds and other relevant information. Furthermore, the implementation of zk-SNARKs allows for the verification of trading strategies without revealing the underlying logic, safeguarding proprietary algorithms and user privacy. The result is a secure, verifiable, and privacy-centric trading solution that gives users complete control over their crypto assets.

QuantCycle is designed with modularity and extensibility in mind. The core engine is built around a flexible architecture that allows for the integration of various trading strategies, risk management protocols, and asset allocation models. The smart contract infrastructure is designed to be compatible with multiple blockchain networks, allowing users to deploy QuantCycle on the blockchain of their choice. This multi-chain support enables access to a wider range of decentralized exchanges and trading opportunities. The user interface (UI) is designed to be intuitive and user-friendly, providing a clear overview of portfolio performance, trading history, and risk metrics. This allows users to monitor their portfolios and make informed adjustments to their trading strategies.

## Key Features

*   **Decentralized Execution:** Trading strategies are executed directly on decentralized exchanges via smart contracts, eliminating the need for centralized intermediaries and ensuring transparency and security.

*   **Smart Contract Oracle Integration:** Leverages Chainlink oracles (or similar decentralized data feeds) to obtain reliable and tamper-proof real-time market data (e.g., price feeds, volatility indices) for informed trading decisions. The contract addresses and data retrieval functions are configurable.

*   **zk-SNARKs for Privacy:** Implements zk-SNARKs to prove the correctness of trading strategy execution without revealing the underlying logic, preserving the confidentiality of proprietary algorithms and user-defined parameters. The proving key and verification key generation process are documented in the `zk-snarks` folder.

*   **Automated Portfolio Rebalancing:** Automatically rebalances portfolio assets based on predefined risk tolerance and investment goals, ensuring optimal asset allocation and risk management. Rebalancing frequency and thresholds are configurable parameters.

*   **Backtesting Framework:** Includes a robust backtesting framework that allows users to simulate trading strategies on historical data, enabling them to evaluate their performance and optimize their parameters before deploying them in a live environment.

*   **Risk Management Controls:** Offers a suite of risk management tools, including stop-loss orders, take-profit orders, and position sizing controls, to mitigate potential losses and protect capital.

*   **Modular Architecture:** Designed with a modular architecture that allows for easy integration of new trading strategies, risk management protocols, and blockchain networks. The strategy interface and abstract classes simplify the addition of new trading logic.

## Technology Stack

*   **TypeScript:** The primary programming language used for developing the trading bot's logic, ensuring type safety and maintainability.
*   **Node.js:** The runtime environment for executing the TypeScript code, enabling server-side execution of the trading bot.
*   **ethers.js/web3.js:** JavaScript libraries for interacting with Ethereum-compatible blockchains, facilitating communication with smart contracts and decentralized exchanges.
*   **Solidity:** The programming language used for developing smart contracts that execute trading strategies on the blockchain.
*   **SnarkJS/Circom:** Tools and languages for designing and implementing zk-SNARKs circuits for privacy-preserving verification.
*   **Chainlink (or similar):** Decentralized oracle network providing reliable and tamper-proof data feeds for market prices and other relevant information.
*   **Jest:** A JavaScript testing framework for writing and executing unit tests and integration tests to ensure the quality and reliability of the codebase.

## Installation

1.  Clone the repository:
    `git clone https://github.com/jjfhwang/QuantCycle.git`

2.  Navigate to the project directory:
    `cd QuantCycle`

3.  Install dependencies:
    `npm install`

4. Install SnarkJS globally:
    `npm install -g snarkjs`

5. Generate proving and verification keys (navigate to the `zk-snarks` folder):
    `snarkjs r1cs generate circuit.circom -o circuit.r1cs`
    `snarkjs zkey new circuit.r1cs pot14_0001.ptau circuit_0000.zkey`
    `snarkjs zkey contribute circuit_0000.zkey circuit_0001.zkey -n="Entropy"`
    `snarkjs zkey export verificationkey circuit_0001.zkey verification_key.json`
    `snarkjs zkey export provingkey circuit_0001.zkey proving_key.json`
    (Note: 'pot14_0001.ptau' can be downloaded from official SnarkJS documentation. Replace circuit.circom with your circuit file name if different.)

## Configuration

1.  Create a `.env` file in the root directory based on the `.env.example` file.

2.  Set the following environment variables:
    *   `WALLET_PRIVATE_KEY`: Your Ethereum wallet private key. (Use a separate wallet for testing and development).
    *   `INFURA_PROJECT_ID`: Your Infura project ID for accessing the Ethereum network.
    *   `CHAINLINK_PRICE_FEED_ADDRESS`: The address of the Chainlink price feed smart contract.
    *   `DEX_ROUTER_ADDRESS`: The address of the decentralized exchange router contract.
    *   `TRADING_STRATEGY`: The path to the trading strategy module to be used. (e.g., `./strategies/simple_ma_crossover.ts`).
    *   `REBALANCING_THRESHOLD`: The percentage threshold for rebalancing the portfolio (e.g., 0.05 for 5%).
    *   `GAS_PRICE`: The gas price to use for transactions (e.g., `10000000000` for 10 Gwei).

## Usage

1.  Compile the TypeScript code:
    `npm run build`

2.  Run the trading bot:
    `npm start`

The trading bot will connect to the Ethereum network, retrieve market data from Chainlink oracles, and execute trading strategies based on the configured parameters. The bot's activity and portfolio performance will be logged to the console.

API documentation for custom strategy creation is available within the `strategies` directory in the form of comments in the abstract strategy class. Extend this class to create your own custom strategies.

## Contributing

We welcome contributions to QuantCycle! Please follow these guidelines:

*   Fork the repository.
*   Create a new branch for your feature or bug fix.
*   Write clear and concise commit messages.
*   Submit a pull request with a detailed description of your changes.
*   Ensure all tests pass before submitting a pull request.
*   Follow the existing code style.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/jjfhwang/QuantCycle/blob/main/LICENSE) file for details.

## Acknowledgements

We would like to thank the following projects and communities for their contributions to the decentralized finance ecosystem:

*   Chainlink
*   Ethereum
*   SnarkJS
*   ethers.js
*   web3.js