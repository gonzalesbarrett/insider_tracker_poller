# **Real-Time SEC Insider Trading Monitor**

This Python script continuously monitors the SEC EDGAR system for new Form 4 filings, which are declarations of insider trading. It parses these filings in real-time, analyzes them for significance based on a configurable scoring system, and sends instant push notifications for high-value trades.

This tool is designed to be run 24/7 on a server (e.g., a free-tier cloud VM) to provide timely alerts on potentially market-moving insider activity.

## **Key Features**

* **Real-Time Monitoring**: Polls the official SEC RSS feed for the latest Form 4 filings as they are published.  
* **Intelligent Parsing**: Extracts key details from filings, including insider's role, trade type (purchase/sale), volume, and price.  
* **Configurable Signal Scoring**: Evaluates trades based on multiple criteria to generate a "Signal Score," helping to filter out noise. Criteria include:  
  * Insider's Role (e.g., CEO, CFO, Director)  
  * Transaction Type (Purchases are weighted heavily)  
  * Absolute dollar value of the trade  
  * Relative trade size as a percentage of the insider's holdings  
  * Trade size vs. the company's market capitalization  
* **Instant Push Notifications**: Uses [Pushover](https://pushover.net/) to send detailed, clickable alerts directly to your phone.  
* **Robust and Lightweight**: Designed to be resilient to parsing errors and run efficiently on low-resource machines.

## **Getting Started**

### **Prerequisites**

* Python 3.8+  
* A Pushover account and app created on your mobile device.

### **Installation**

1. **Clone the Repository:**  
   git clone \[https://github.com/your-username/your-repository-name.git\](https://github.com/your-username/your-repository-name.git)  
   cd your-repository-name

2. **Create and Activate a Virtual Environment:**  
   python3 \-m venv venv  
   source venv/bin/activate

3. **Install Required Packages:**  
   pip install \-r requirements.txt

   *(Note: You will need to create a requirements.txt file with the following content):*  
   requests  
   yfinance

### **Configuration**

Before running the script, you must edit the Insider\_Tracker\_Poller.py file and update the configuration section at the top:

1. **SEC\_USER\_AGENT**: The SEC requires a descriptive User-Agent. Change the placeholder to your own project name and email.  
   SEC\_USER\_AGENT \= "My Insider Trading Project my.email@example.com"

2. **PUSHOVER\_USER\_KEY and PUSHOVER\_API\_TOKEN**:  
   * Find your **User Key** on your main Pushover dashboard.  
   * Create a new **Application** on the Pushover site to get an **API Token**.  
   * Paste both keys into their respective variables in the script.

PUSHOVER\_USER\_KEY \= "PASTE\_YOUR\_USER\_KEY\_HERE"  
PUSHOVER\_API\_TOKEN \= "PASTE\_YOUR\_API\_TOKEN\_HERE"

3. **ALERT\_THRESHOLD (Optional)**: Adjust the sensitivity of the alerts. The default is 7.0. A higher value will result in fewer, more significant notifications.

## **Usage**

To run the script, simply execute it from your terminal while your virtual environment is active:

python3 Insider\_Tracker\_Poller.py

For continuous 24/7 operation, it is recommended to run the script inside a terminal multiplexer like screen or tmux on a server.

\# Start a new detached screen session named 'scraper'  
screen \-dmS scraper python3 Insider\_Tracker\_Poller.py

\# To re-attach to the session later and view the output  
screen \-r scraper

## **Disclaimer**

This tool is for informational and educational purposes only. The data is sourced directly from the SEC, but no guarantee is made about its accuracy or timeliness. The output of this script should not be considered financial advice. Always do your own research before making any investment decisions.
