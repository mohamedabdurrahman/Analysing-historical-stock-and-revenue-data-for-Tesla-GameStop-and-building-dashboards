# Analysing-historical-stock-and-revenue-data-for-Tesla-GameStop-and-building-dashboards
Analysing historical stock and revenue data for Tesla &amp; GameStop and building dashboards

Project Overview

This project focuses on analyzing historical stock prices and quarterly revenue data for Tesla (TSLA) and GameStop (GME). We extract stock data using Yahoo Finance and revenue data using web scraping. Finally, we visualize trends and create dashboard-ready plots.

### Key Objectives

1. Extract Tesla stock data using `yfinance`.
2. Extract Tesla revenue data from the web using `BeautifulSoup`.
3. Extract GameStop stock data using `yfinance`.
4. Extract GameStop revenue data from the web.
5. Create a **Tesla stock and revenue dashboard**.
6. Create a **GameStop stock and revenue dashboard**.

---

## Data Sources

- **Yahoo Finance** for historical stock prices.
- **Course-provided HTML pages** for quarterly revenue:
  - Tesla: [link](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm)
  - GameStop: [link](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html)

---


## Project Structure

Analysing-historical-stock-and-revenue-data-for-Tesla-GameStop-and-building-dashboards-project
│
├── README.md
├── Analysing-historical-stock-and-revenue-data-for-Tesla-GameStop-and-building-dashboards.ipynb
├── plots/
│   ├── tesla_historical_share_price.pdf
│   ├── tesla_revenue.pdf
│   ├── gamestop_historical_share_price.pdf
│   └── gamestop_revenue.pdf

---

## Project Files

- `Analysing historical stock and revenue data for Tesla & GameStop and building dashboards.ipynb` – Notebook with all analysis, visualizations, and dashboards.
- `plots/` – screenshots of stock and revenue plots for Tesla & GameStop.


---

# Analysing historical stock and revenue data for Tesla & GameStop and building dashboards Project


 -----------------------------
 Import libraries
 -----------------------------
import pandas as pd
import yfinance as yf
import requests
from bs4 import BeautifulSoup
!pip install --upgrade plotly

 -----------------------------
 Extracting Tesla Stock Data Using yfinance
 -----------------------------
import yfinance as yf

tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)
tesla_data.head()

 -----------------------------
 Extracting Tesla Revenue Data Using Webscraping
 -----------------------------
     
    import pandas as pd
import requests
from bs4 import BeautifulSoup

 Load the webpage
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"
html_data = requests.get(url).text

 Parse the HTML
soup = BeautifulSoup(data, "html.parser")

 Locate the Tesla quarterly revenue table (second tbody on the page)
table = soup.find_all("tbody")[1]

 Create an empty DataFrame
tesla_revenue = pd.DataFrame(columns=["Date", "Revenue"])

 Loop through all rows in the table
for row in table.find_all("tr"):
    cols = row.find_all("td")
    if len(cols) == 2:
        date = cols[0].text.strip()
        revenue = cols[1].text.strip()
        tesla_revenue = pd.concat([
            tesla_revenue,
            pd.DataFrame({"Date": [date], "Revenue": [revenue]})
        ], ignore_index=True)

 Clean up the revenue column
tesla_revenue["Revenue"] = tesla_revenue["Revenue"].str.replace(',|\$', '', regex=True)
tesla_revenue.dropna(inplace=True)
tesla_revenue = tesla_revenue[tesla_revenue["Revenue"] != ""]

 Display the last 5 rows
tesla_revenue.tail()

    
 -----------------------------
 Extracting GameStop Stock Data Using yfinance
 -----------------------------

import yfinance as yf

gme = yf.Ticker("GME")
gme_data = gamestop.history(period="max")
gme_data.reset_index(inplace=True)
gme_data.head()

 -----------------------------
 Extracting GameStop Revenue Data Using Webscraping
 -----------------------------
 import pandas as pd
import requests
from bs4 import BeautifulSoup

 Load the webpage
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"
html_data_2 = requests.get(url).text

 Parse the HTML
soup = BeautifulSoup(data, "html.parser")

 Locate the GME quarterly revenue table (second tbody on the page)
tbodies = soup.find_all("tbody")
GamesStop_quarterly_table = tbodies[1]

 Create an empty DataFrame
gme_revenue = pd.DataFrame(columns=["Date", "Revenue"])

 Loop through all rows in the table
for row in table.find_all("tr"):
    cols = row.find_all("td")
    if len(cols) == 2:
        date = cols[0].text.strip()
        revenue = cols[1].text.strip()
        gme_revenue = pd.concat([
            gme_revenue,
            pd.DataFrame({"Date": [date], "Revenue": [revenue]})
        ], ignore_index=True)

 Clean up the revenue column
gme_revenue["Revenue"] = gme_revenue["Revenue"].str.replace(',|\$', '', regex=True)
gme_revenue.dropna(inplace=True)
gme_revenue = gme_revenue[gme_revenue["Revenue"] != ""]

 Display the last 5 rows
gme_revenue.tail()

 -----------------------------
 Tesla Stock and Revenue Dashboard
 -----------------------------
make_graph(tesla_data, tesla_revenue, 'Tesla')

 -----------------------------
 GameStop Stock and Revenue Dashboard
 -----------------------------
make_graph(gme_data, gme_revenue, 'GameStop')


# Dashboards Preview
<img width="517" height="328" alt="Q5" src="https://github.com/user-attachments/assets/2b8a84e5-e472-4715-a62e-92c680ff5508" />
<img width="551" height="331" alt="Q5 1" src="https://github.com/user-attachments/assets/e6157567-d4fa-4dbf-96e4-acf9ad554cd1" />
<img width="555" height="337" alt="Q6" src="https://github.com/user-attachments/assets/25ebe50f-499f-42cf-a8bf-b0a978c461b1" />
<img width="565" height="319" alt="Q6 1" src="https://github.com/user-attachments/assets/0b4d01b3-784b-4157-aec4-c381550158cf" />




