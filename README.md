# QuantCycle - Streamlining Quantitative Finance Workflows

QuantCycle is a robust TypeScript library designed to accelerate the development and deployment of quantitative finance strategies and models. It provides a comprehensive suite of tools and functionalities, empowering developers to efficiently manage data acquisition, pre-processing, analysis, and backtesting within a unified framework. QuantCycle aims to reduce the boilerplate often associated with quantitative development, allowing quants and developers to focus on the core logic and innovation of their models.

This library addresses the common challenges faced in quantitative finance projects: fragmented toolchains, complex data handling, and the need for rapid prototyping. QuantCycle consolidates these disparate components into a cohesive system. By offering pre-built modules for common tasks such as fetching market data, performing technical analysis, and implementing backtesting simulations, QuantCycle streamlines the development process from initial concept to production-ready implementation. The use of TypeScript ensures type safety and maintainability, contributing to the long-term robustness and reliability of quantitative models built with this library.

The core philosophy of QuantCycle is to provide a flexible and extensible platform. It allows for the seamless integration of custom algorithms and data sources, ensuring that the library can adapt to the evolving needs of individual projects. The modular architecture promotes code reusability and simplifies the process of building complex quantitative models. Furthermore, QuantCycle's comprehensive documentation and example code serve as a valuable resource for both novice and experienced quantitative developers, facilitating a quick and effective learning curve.

## Key Features

*   **Data Acquisition Module:** Provides interfaces and abstract classes for connecting to various data sources (e.g., REST APIs, WebSocket streams, database connections). Supports customizable data retrieval and caching mechanisms. Implementations for common data providers will be added in future releases. `Example: const dataProvider = new GenericDataProvider('https://api.example.com/data', { ticker: 'AAPL' }); const data = await dataProvider.getData();`
*   **Technical Analysis Indicators:** Includes a library of pre-built technical indicators (e.g., Moving Averages, RSI, MACD) with optimized implementations for performance. Easily extendable with custom indicators. `Example: const rsi = new RSI(14); const rsiValues = rsi.calculate(closingPrices);`
*   **Backtesting Engine:** Offers a flexible backtesting framework with support for different order execution models, risk management strategies, and performance metrics. Enables comprehensive evaluation of trading strategies. Features vectorized backtesting capabilities for increased speed. `Example: const backtester = new Backtester(strategy, historicalData, initialCapital); const results = await backtester.run();`
*   **Order Management System:** Provides an abstraction layer for interacting with different brokerage APIs. Simplifies the process of placing, modifying, and canceling orders. Supports paper trading and live trading environments. `Example: const order = new Order('AAPL', 100, OrderType.MARKET, OrderSide.BUY); broker.placeOrder(order);`
*   **Risk Management Module:** Implements various risk management techniques, including position sizing, stop-loss orders, and portfolio diversification. Helps to control risk exposure and maximize returns. `Example: const stopLoss = new StopLoss(0.05); stopLoss.apply(position);`
*   **Portfolio Optimization Tools:** Includes algorithms for optimizing portfolio allocation based on risk and return objectives. Supports various optimization methods, such as Mean-Variance Optimization and Black-Litterman Model. `Example: const optimizer = new MeanVarianceOptimizer(expectedReturns, covarianceMatrix); const optimalWeights = optimizer.optimize();`

## Technology Stack

*   **TypeScript:** Provides static typing and modern JavaScript features, ensuring code maintainability and scalability.  TypeScript enables robust code completion and error detection during development.
*   **Node.js:** A JavaScript runtime environment that allows for server-side execution of TypeScript code. Crucial for building backtesting engines and data processing pipelines.
*   **npm (Node Package Manager):** Used for managing project dependencies and installing required packages. Facilitates easy integration of third-party libraries.
*   **Jest:** A popular testing framework for ensuring the quality and reliability of the code. Facilitates unit and integration testing.
*   **(Optional) Redis:** Can be used for caching frequently accessed data to improve performance. Enables faster data retrieval and reduced load on data sources.

## Installation

1.  **Prerequisites:** Ensure you have Node.js (version 16 or higher) and npm installed on your system. You can download them from the official Node.js website.
2.  **Clone the repository:**
    `git clone https://github.com/jjfhwang/QuantCycle.git`
3.  **Navigate to the project directory:**
    `cd QuantCycle`
4.  **Install dependencies:**
    `npm install`

## Configuration

The project uses environment variables for configuration. Create a `.env` file in the root directory of the project. The following environment variables can be configured:

*   `DATA_API_KEY`: API key for accessing market data (required if using a data provider that requires an API key).
*   `BROKERAGE_API_KEY`: API key for connecting to your brokerage account (required for live trading).
*   `REDIS_HOST`: Hostname of the Redis server (optional, defaults to localhost).
*   `REDIS_PORT`: Port number of the Redis server (optional, defaults to 6379).

Example `.env` file:

DATA_API_KEY=your_data_api_key
BROKERAGE_API_KEY=your_brokerage_api_key
REDIS_HOST=localhost
REDIS_PORT=6379

## Usage

1.  **Import the necessary modules:**

import { Backtester, RSI, GenericDataProvider } from 'quantcycle';

2.  **Create a data provider:**

const dataProvider = new GenericDataProvider('https://api.example.com/historical_data', { ticker: 'AAPL', startDate: '2023-01-01', endDate: '2023-01-31' });
const historicalData = await dataProvider.getData();

3.  **Implement a trading strategy:**

function strategy(data: any[], rsiThreshold: number = 30) {
  const rsi = new RSI(14);
  const rsiValues = rsi.calculate(data.map(item => item.close));

  const signals: string[] = [];
  for (let i = 1; i < data.length; i++) {
    if (rsiValues[i] < rsiThreshold && rsiValues[i - 1] >= rsiThreshold) {
      signals.push('BUY');
    } else if (rsiValues[i] > (100 - rsiThreshold) && rsiValues[i - 1] <= (100-rsiThreshold)){
        signals.push('SELL');
    }
    else {
      signals.push('HOLD');
    }
  }
  return signals;
}

4.  **Run the backtester:**

const initialCapital = 10000;
const backtester = new Backtester(strategy, historicalData, initialCapital);
const results = await backtester.run();

5.  **Access the backtesting results:**

console.log(results);

Detailed API documentation will be provided in a separate document in the `/docs` directory. This will cover all classes, methods, and interfaces available in the library.

## Contributing

We welcome contributions to QuantCycle! Please follow these guidelines:

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Write clear, concise, and well-documented code.
4.  Write unit tests for your changes.
5.  Submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/jjfhwang/QuantCycle/blob/main/LICENSE) file for details.

## Acknowledgements

We would like to acknowledge the contributions of the open-source community to the development of this library. Specifically, the developers of TypeScript, Node.js, and other related technologies.