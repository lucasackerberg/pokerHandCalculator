# PokerHandsCalculator

PokerHandsCalculator is a web application built with Vue.js and Laravel that calculates poker hand winning percentages and equity at different stages of the game (pre-flop, flop, turn, and river). This tool is designed to help poker players make informed decisions by analyzing the strength of their hands in various scenarios.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Hand Equity Calculation**: Calculate the winning percentage and equity of any poker hand.
- **Stage Analysis**: Evaluate hand strength at different stages of a poker game (pre-flop, flop, turn, river).
- **User-Friendly Interface**: Simple and intuitive UI built with Vue.js.
- **Backend Calculations**: Utilizes Laravel for efficient backend processing and calculations.
- **Real-Time Updates**: Instant feedback and updates as you input different hands and scenarios.

## Contributing
Contributions are welcome! Please follow these steps to contribute:

Fork the repository.
Create a new branch.
Commit your changes.
Push to the branch.
Open a Pull Request.

## Installation

To get started with PokerHandsCalculator, follow these steps:

### Prerequisites

Make sure you have the following software installed:

- [Node.js](https://nodejs.org/) (version 12.x or later)
- [NPM](https://www.npmjs.com/) (Node Package Manager)
- [Composer](https://getcomposer.org/) (PHP dependency manager)
- [PHP](https://www.php.net/) (version 7.4 or later)

Clone the repository!

Backend Setup (Laravel)
Install Dependencies:

bash
```
composer install
```

Copy the .env File:
```
cp .env.example .env
```

Generate Application Key:
```
php artisan key:generate
```

Configure Environment Variables:

Update the .env file with your database credentials and other necessary settings.

Run Migrations:
```
php artisan migrate
```

Start the Laravel Development Server:
```
php artisan serve
```

Install Dependencies:
```
npm install
```

Compile and Hot-Reload for Development:
```
npm run serve
```
