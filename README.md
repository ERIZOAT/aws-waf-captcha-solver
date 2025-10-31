# AWS WAF CAPTCHA Solver (Image & Token)

![](https://assets.capsolver.com/prod/posts/auto-aws-waf-captcha-solve/yudGDPtinhla-f16adf374ac59d97175e7de4f4a4c626.png)

## 🚀 Overview

This repository provides a focused guide on using the **CapSolver** API to automatically solve **AWS WAF CAPTCHA** challenges. This solution is crucial for web scraping and automation tasks targeting sites protected by AWS Web Application Firewall.

AWS WAF CAPTCHA primarily presents two types of challenges: **Image Recognition** and **Token-Based Verification** (`aws-waf-token`). CapSolver provides dedicated task types for both.

## 💡 Key Features

| Challenge Type | CapSolver Task Type | Primary Use Case |
| :--- | :--- | :--- |
| **Token-Based** | `AntiAwsWafTask` / `AntiAwsWafTaskProxyLess` | Scalable, high-volume token generation |
| **Image Recognition** | `AwsWafClassification` | Solving image puzzles (e.g., "Select all chairs") |

## 🛠️ API Integration Guide

For scalable, production-ready automation, direct API integration is recommended.

### Prerequisites

1.  **CapSolver Account:** Get your API Key from the [CapSolver Dashboard](https://dashboard.capsolver.com/dashboard/overview/?utm_source=github&utm_medium=readme).
2.  **Required Parameters:** You must extract parameters like `awsKey`, `awsIv`, and `awsContext` from the target page's source code to solve token-based challenges.

### 1. Solving Token-Based Challenges (`aws-waf-token`)

This method is for generating the required `aws-waf-token` cookie to bypass the WAF.

**API Request Example (`AntiAwsWafTaskProxyLess`):**

```json
{
  "clientKey": "YOUR_API_KEY",
  "task": {
    "type": "AntiAwsWafTaskProxyLess",
    "websiteURL": "https://your-target-website.com",
    "awsKey": "...",
    "awsIv": "...",
    "awsContext": "..."
  }
}
```

**Result:** The API returns the valid `aws-waf-token` in the `cookie` field of the solution.

### 2. Solving Image Recognition Challenges

This method is for solving visual puzzles.

**API Request Example (`AwsWafClassification`):**

```json
{
  "clientKey": "YOUR_API_KEY",
  "task": {
    "type": "AwsWafClassification",
    "websiteURL": "https://your-target-website.com",
    "images": ["/9j/4AAQSkZJRgAB..."], // Base64 encoded image
    "question": "aws:grid:chair" // The question
  }
}
```

**Result:** The API returns the coordinates or indices of the correct images.

## 💻 Browser Automation Integration (Low-Code)

For smaller tasks or integration with existing browser automation frameworks (Puppeteer/Selenium), the CapSolver extension can be loaded directly.

### Node.js (Puppeteer) Example

```javascript
const puppeteer = require("puppeteer");

(async () => {
  const pathToExtension = "/path/to/your/capsolver_extension_folder"; // Update path
  const browser = await puppeteer.launch({
    headless: false,
    args: [`--disable-extensions-except=${pathToExtension}`, `--load-extension=${pathToExtension}`],
  });
  const page = await browser.newPage();
  await page.goto("https://your-target-website.com"); // WAF Protected
})();
```

### Python (Selenium) Example

```python
from selenium import webdriver

chrome_options = webdriver.ChromeOptions()
chrome_options.add_extension("./capsolver_extension.zip")  # Path to the zipped extension
driver = webdriver.Chrome(options=chrome_options)
driver.get("https://your-target-website.com") # WAF Protected
```

## 🎁 Bonus Code

Redeem code **CAP25** on the [CapSolver Dashboard](https://dashboard.capsolver.com/dashboard/overview/?utm_source=github&utm_medium=readme) to get an extra 5% bonus on every recharge (unlimited).

## 🔗 Resources & Documentation

*   [CapSolver Documentation](https://www.capsolver.com/products/awswaf/?utm_source=github&utm_medium=readme)
*   [AWS WAF Captcha Token Docs](https://docs.capsolver.com/en/guide/captcha/awsWaf/)
*   [AWS WAF Images Recognize Docs](https://docs.capsolver.com/en/guide/recognition/AwsWafClassification/)
*   [Dashboard Login](https://dashboard.capsolver.com/dashboard/overview/?utm_source=github&utm_medium=readme)
