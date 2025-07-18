# 📊 Analysis: Wallet Credit Score Distribution & Behavior

This document provides insights into the distribution of credit scores and the behavioral patterns of wallets in different score segments based on their interactions with the Aave V2 protocol.

---

## 📌 Score Distribution

We group scores into bins of 100 and count the number of wallets in each range:

| Score Range | Number of Wallets |
| ----------- | ----------------- |
| 0–100       | ████▌             |
| 100–200     | ███████▉          |
| 200–300     | █████████▎        |
| 300–400     | ██████████▍       |
| 400–500     | ███████████▎      |
| 500–600     | ███████████       |
| 600–700     | █████████▉        |
| 700–800     | ████████▍         |
| 800–900     | ██████▎           |
| 900–1000    | ██▉               |

*A histogram of this distribution is plotted in the notebook.*

---

## 🔍 Low Score Wallets (0–200)

Characteristics:

* High number of **borrows** without corresponding **repays**
* One or more **liquidationcall** events
* Very **short active durations** (often single-day usage)
* Low deposit frequency

Interpretation:
These wallets show risk-seeking behavior, poor repayment discipline, and often exit the protocol early—potential indicators of bots, airdrop farmers, or malicious actors.

---

## 🏅 High Score Wallets (800–1000)

Characteristics:

* Consistent **deposit and repay** behavior
* Little to no **liquidation** events
* Long **active duration** (weeks or months)
* Low borrow-to-repay ratio (indicating responsible borrowing)

Interpretation:
These are likely to be long-term users, potentially using Aave for stable collateral management or yield generation. Their activity indicates trustworthiness and protocol-friendly behavior.

---

## 🧠 Observations

* The score distribution is **center-heavy**, indicating most wallets fall into the 300–700 range.
* **Outliers** on the low-end often show high liquidation and sparse activity.
* **Outliers** on the high-end often show very regular deposits and consistent repayments.

---

## 📈 Recommendations

* Score can be used for user segmentation: e.g., flag risky wallets under 300, reward top-tier wallets over 800.
* Incorporate temporal velocity features (how quickly a wallet repays or borrows) in future versions.

---

Generated from \~100K raw transaction records on the Aave V2 protocol.
