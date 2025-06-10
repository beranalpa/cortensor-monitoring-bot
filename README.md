# 🤖 Cortensor Monitoring Bot

A powerful Telegram bot designed to provide comprehensive monitoring and alerting for Cortensor nodes. Keep track of your node's health, statistics, and transaction status with on-demand reports and proactive, real-time alerts.

## ✨ Key Features

-   **Comprehensive Node Statistics:** Get detailed reports on points, success rates, and performance trends over 1-hour and 24-hour periods.
-   **Real-Time Health Checks:** Instantly check your node's operational status, latest transaction, and balance.
-   **Live-Updating Reports:** Start an auto-updating message in your chat that provides a live look at your node's stats.
-   **Automatic Failed Transaction Alerts:** Receive proactive, near real-time notifications the moment one of your nodes has a failed transaction.
-   **Multi-Node Management:** Register and manage multiple nodes seamlessly from a single Telegram chat.

## 🛠️ Setup & Installation

To get the bot running, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/beranalpa/cortensor-monitoring-bot.git
    cd cortensor-monitoring-bot
    ```

2.  **Install dependencies:**
    Make sure you have Python 3.8+ installed.
    ```bash
    pip install -r requirements.txt
    ```
    *(If you don't have a `requirements.txt` file, install the necessary libraries manually)*:
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

## 🤖 Commands Guide

Here is a complete list of all available commands.

### **1. Getting Started**

These commands help you get started and view the command list.

**`/start`** or **`/help`**
-   **Function:** Displays the full list of available commands and their descriptions.
-   **Usage:** Simply send `/start` or `/help`.

### **2. Managing Your Nodes**

Use these commands to add or remove the node addresses you want to monitor.

**`/register`**
-   **Function:** Registers a new node address for monitoring and assigns it a custom, easy-to-remember name.
-   **Usage:** `/register <your_address> <your_custom_name>`
-   **Example:** `/register 0x123abcde...fghij Node 1`

**`/unregister`**
-   **Function:** Removes a previously registered node from your monitoring list.
-   **Usage:** `/unregister <the_address_to_remove>`
-   **Example:** `/unregister 0x123abcde...fghij`

**`/list`**
-   **Function:** Shows a complete list of all the node addresses you are currently monitoring.
-   **Usage:** `/list`

### **3. Manual Monitoring**

These commands provide on-demand reports for your nodes.

**`/stats`**
-   **Function:** Generates a detailed statistics report card. This includes total points, success rates, and performance changes over the last 1 and 24 hours.
-   **Usage:**
    -   `/stats` - To get reports for all your registered nodes.
    -   `/stats <address>` - To get a report for one specific node.

**`/health`**
-   **Function:** Provides a real-time health check of a node, including its status (Active/Inactive), balance, and a health bar representing its most recent transactions.
-   **Usage:**
    -   `/health` - To check all your registered nodes.
    -   `/health <address>` - To check one specific node.

### **4. Live Stats Automation**

This feature provides a "live" dashboard that updates automatically in your chat.

**`/autoupdate`**
-   **Function:** Starts a live stats report. The bot will send an initial report card and then automatically edit that same message with fresh data at the interval you specify.
-   **Usage:** `/autoupdate <interval_in_seconds>`
-   **Example:** `/autoupdate 300` (This will update the report every 5 minutes).
-   **Note:** The minimum interval is 60 seconds. Starting a new `/autoupdate` job will automatically stop and clean up the previous one.

**`/stop`**
-   **Function:** Stops the live-updating stats report that was started by `/autoupdate`.
-   **Usage:** `/stop`

### **5. Automatic Transaction Alerts**

This system monitors your nodes in the background and alerts you proactively if something goes wrong.

**`/auto`**
-   **Function:** Turns **ON** the automatic alert system. The bot will monitor your nodes 24/7 and send you an immediate notification if a recent transaction fails.
-   **Usage:** `/auto`

**`/off`**
-   **Function:** Turns **OFF** the automatic alert system. You will no longer receive proactive alerts for failed transactions.
-   **Usage:** `/off`
