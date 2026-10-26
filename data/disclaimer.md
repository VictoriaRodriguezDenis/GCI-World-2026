# Dataset instructions

The notebook expects the following source files:

- `Client.csv` — customer/account attributes; must contain `Customer_ID`.
- `Record.csv` — usage records and churn target; must contain `Customer_ID` and binary `churn` (`0` = stayed, `1` = churned).

The notebook searches the current working directory, a local `data/` directory, the repository's `data/` directory, and `/content` (commonly used by Colab).

The original source data is not included because I am unsure if I am authorized to share it. For this reason, I chose to create my own dataset based on the work presented in this repository.
