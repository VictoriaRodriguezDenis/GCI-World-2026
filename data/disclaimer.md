# Dataset instructions

The notebook expects the following source files:

- `Client.csv` — customer/account attributes; must contain `Customer_ID`.
- `Record.csv` — usage records and churn target; must contain `Customer_ID` and binary `churn` (`0` = stayed, `1` = churned).

The notebook searches the current working directory, a local `data/` directory, the repository's `data/` directory, and `/content` (commonly used by Colab).

The source data is not included. Before obtaining, storing, or publishing it, verify the course/provider's terms and license. Do not commit personal, confidential, or otherwise restricted customer data. If redistribution is not permitted, document the authorized source and access process without uploading the files.
