# 🏦 Aave V2 Wallet Credit Scoring

This project builds a credit scoring system (range: 0 to 1000) for wallets interacting with the Aave V2 DeFi lending protocol. The score represents the historical reliability and riskiness of a wallet based on its transaction behavior.

---

## 📌 Problem Statement

Using raw transaction-level data (\~100K records), generate a credit score for each wallet address based on activity types such as deposits, borrows, repayments, liquidations, and redemptions.

---

## 🧠 Approach

We use a rule-based (heuristic) scoring strategy in this version. The idea is to reward responsible DeFi usage (repayment, regular activity) and penalize riskier patterns (excessive borrowing, liquidations).

Each wallet's history is summarized into a set of behavioral features, scored via a simple weighted formula, and then scaled to the standard 0–1000 credit range.

---

## 📊 Features Engineered

| Feature        | Description                           |
| -------------- | ------------------------------------- |
| total\_txn     | Total transactions by wallet          |
| total\_deposit | Number of deposit actions             |
| total\_borrow  | Number of borrow actions              |
| total\_repay   | Number of repay actions               |
| liquidations   | Number of times liquidated            |
| avg\_amount    | Mean transaction value                |
| active\_days   | Days active between first and last tx |

---

## 📈 Scoring Formula (Heuristic)

```python
score_raw = (
    2 * total_deposit +
    3 * total_repay +
    1 * active_days -
    5 * liquidations -
    1 * total_borrow
)
```

Then scaled to \[0–1000] using min-max normalization.

---

## 🗂️ Files & Structure

```
├── score_generator.py       # One-step scoring script
├── notebook.ipynb           # Step-by-step explanation & scoring in Colab
├── wallet_scores.csv        # Output file with wallet + score
├── analysis.md              # Score distribution + wallet behavior analysis
├── README.md                # Project overview
```

---

## 🚀 How to Run

1. Upload the provided `user-transactions.json` file (87MB).
2. Run the `notebook.ipynb` or `score_generator.py` script.
3. It will generate a `wallet_scores.csv` with user addresses and scores.

---

## 🧪 Sample Output

| user          | score |
| ------------- | ----- |
| 0x1234abcd... | 745   |
| 0xabcd5678... | 220   |

---

## 📦 Requirements

* Python 3.7+
* Libraries:

  * pandas
  * numpy
  * matplotlib
  * seaborn
  * scikit-learn

Install via:

```bash
pip install -r requirements.txt
```

---

## 📌 Future Work

* Add unsupervised learning (e.g., KMeans or DBSCAN)
* Model repayment ratios vs. borrow ratios over time
* Integrate DeFi protocol metadata (e.g., asset risk classes)
* Apply wallet clustering to detect bots / spam actors

---

## 📄 License

MIT License. This is an open challenge submission.

---

Built for the **Aave Credit Scoring Challenge 2025** 🛠️
