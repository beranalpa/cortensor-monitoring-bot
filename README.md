<div align="center">

  <img src="https://avatars.githubusercontent.com/u/174224856?s=200&v=4" alt="Project Banner">
<h1>Cortensor Monitoring Bot</h1>

<p>
A sophisticated and feature-rich Telegram bot for comprehensive monitoring and real-time alerting of Cortensor nodes.
</p>
 <p>
    <a href="https://github.com/your-username/cortensor-watcher-bot/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"></a>
    <a href="#"><img src="https://img.shields.io/badge/status-active-success.svg" alt="Status"></a>
    <a href="#"><img src="https://img.shields.io/badge/python-3.11+-blue.svg" alt="Python Version"></a>
    <a href="#"><img src="https://img.shields.io/badge/docker-%230db7ed.svg?logo=docker&logoColor=white" alt="Docker"></a>
  </p>

</div>

---

## 📄 Table of Contents

- [About The Project](#-about-the-project)
- [✨ Key Features](#-key-features)
- [📸 Screenshots](#-screenshots)
- [🚀 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [🤖 Command Guide](#-command-guide)
- [⚙️ How It Works](#️-how-it-works)
- [📜 License](#-license)

## 📖 About The Project

**Cortensor Monitoring Bot** is more than just a simple monitoring tool. It's a proactive assistant designed to give node operators peace of mind. It provides detailed, on-demand reports, live-updating dashboards directly in your chat, and a near real-time alerting system for critical events like failed transactions.

With a persistent database and intelligent background tasks, this bot ensures you are always informed about your node's performance and health.

## ✨ Key Features

-   **Comprehensive Monitoring:** A single `/stats` command provides a unified report with points, success rates, balance, health status, and more.
-   **Historical Performance Tracking:** Automatically tracks and displays node performance changes over **15-minute, 1-hour, and 24-hour** intervals.
-   **Dynamic Health Bar:** A visual health bar dynamically represents the success/failure of all transactions within the last 30 minutes.
-   **Near Real-Time Alerts:** A background job runs every minute to check for recently failed transactions and sends an immediate, detailed notification if one is found.
-   **User Control:** Users can enable or disable automatic alerts at any time using the `/auto` and `/off` commands.
-   **Live Reports:** The `/autoupdate` command creates a "live" report card in your chat that continuously edits itself with the latest data.
-   **Smart Cleanup:** The bot automatically cleans up old report messages when you request new ones, keeping your chat tidy.
-   **Multi-Node Management:** Easily register, unregister, and list multiple nodes to monitor from a single account.

## 📸 Screenshots

#### Comprehensive Stats Report
This report combines all vital statistics, health information, and performance trends into a single, easy-to-read card.
*(Your screenshot of the `/stats` output goes here)*

#### Proactive Failed Transaction Alert
Receive immediate, detailed alerts when something goes wrong.
*(Your screenshot of the automatic alert message goes here)*

## 🚀 Getting Started

Follow these steps to get your own instance of the bot running.

### Prerequisites

-   Python 3.9 or higher
-   A Telegram Bot Token obtained from [@BotFather](https://t.me/BotFather)
-   An Arbiscan API Key

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/beranalpa/cortensor-monitoring-bot.git
    cd cortensor-monitoring-bot
    ```

2.  **Install dependencies:**
    It's recommended to use a virtual environment.
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```
    *(If a `requirements.txt` file is not available, install manually)*:
    ```bash
    pip install aiogram apscheduler aiohttp python-dotenv
    ```

3.  **Configure Environment Variables:**
    Create a file named `.env` in the root directory of the project and add your secret keys:
    ```env
    TELEGRAM_TOKEN="YOUR_TELEGRAM_BOT_TOKEN_HERE"
    ARBISCAN_API_KEY="YOUR_ARBISCAN_API_KEY_HERE"
    ```

4.  **Run the bot:**
    ```bash
    python3 main.py
    ```
    The bot will start, initialize the databases, and schedule the background jobs.

## 🤖 Command Guide

The following table provides a quick reference for all available commands.

| Command | Arguments | Description |
| :--- | :--- | :--- |
| **`/start`**, **`/help`** | *(none)* | Displays the main help message. |
| **`/register`** | `<address> <name>` | Registers a new node with a custom name. |
| **`/unregister`** | `<address>` | Removes a registered node from your list. |
| **`/list`** | *(none)* | Shows all nodes you are currently monitoring. |
| **`/stats`** | `[address]` | Generates a comprehensive report for your node(s). |
| **`/health`** | `[address]` | Provides a concise, real-time health check. |
| **`/autoupdate`** | `<seconds>` | Starts a live-updating report in your chat. |
| **`/stop`** | *(none)* | Stops and cleans up the live-updating report. |
| **`/auto`** | *(none)* | **Enables** automatic failed transaction alerts. |
| **`/off`** | *(none)* | **Disables** automatic failed transaction alerts. |

## ⚙️ How It Works

The bot utilizes a powerful scheduler (`APScheduler`) to run two key background tasks independently of user commands:

1.  **Historical Data Logger:** Every **15 minutes**, the bot fetches the entire Cortensor leaderboard, aggregates the data for every miner, and saves a snapshot into a local SQLite database (`history.db`). This data is crucial for calculating the performance trends shown in the `/stats` report.

2.  **Failed Transaction Alerter:** Every **1 minute**, the bot checks the most recent transactions for all registered nodes (for users who have alerts enabled). It specifically looks for transactions that have failed within the last 5 minutes and have not been alerted before, ensuring timely and relevant notifications.

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
