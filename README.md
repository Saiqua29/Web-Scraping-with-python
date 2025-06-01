
# 📊 Web Scraping a Wikipedia page showing a list of largest companies in India 

![Webscraping in Python](https://github.com/Saiqua29/Web-Scraping-with-python/blob/main/web%20scraping.jpg)

This project demonstrates how to **scrape structured data from a Wikipedia page** using Python and convert it into a clean, usable CSV file using the `BeautifulSoup`, `requests`, and `pandas` libraries.

---

## 🏷️ Common Badges

![Python](https://img.shields.io/badge/python-3.10+-blue)
![License](https://img.shields.io/badge/license-MIT-blue)
![Last Commit](https://img.shields.io/github/last-commit/Saiqua29/Web-Scraping-with-python)
![Repo Size](https://img.shields.io/github/repo-size/Saiqua29/Web-Scraping-with-python)
![Issues](https://img.shields.io/github/issues/Saiqua29/Web-Scraping-with-python)


---

## 🔍 Objective

To extract a table listing the **largest companies in India** from Wikipedia and save it as a CSV file for further analysis.

---

## 🧰 Technologies Used

- Python 3
- [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Requests](https://docs.python-requests.org/en/latest/)
- [Pandas](https://pandas.pydata.org/)

---

## 📌 Steps Performed

### 1. Import Required Libraries

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

### 2. Define the Target URL

```python
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_India'
```

### 3. Request and Parse the Webpage

```python
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html.parser')
```

### 4. Locate the Desired Table

```python
table = soup.find('table', class_='wikitable sortable')
```

### 5. Extract Table Headers

```python
world_titles = table.find_all('th')
world_table_titles = [title.text.strip() for title in world_titles]
print(world_table_titles)
```

### 6. Create a DataFrame with the Extracted Headers

```python
df = pd.DataFrame(columns=world_table_titles)
```

### 7. Extract Each Row of Data and Append to DataFrame

```python
column_data = table.find_all('tr')

for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = individual_row_data
```

### 8. Export Data to CSV

```python
df.to_csv(r'C:\python webscraping\companies_2021.csv', index=False)
```

> Make sure the folder `C:\python webscraping\` exists before running this script.

### 9. Optional: Use `pandas.read_html()` Directly

```python
pd.read_html('https://en.wikipedia.org/wiki/List_of_largest_companies_in_India')[0]
```

---

## 📁 Output

The final output is a CSV file:

```
companies_2021.csv
```

---

## 📊 Sample Output (Preview of CSV)

| Rank | Name                      | Industry     | Revenue (₹ crore) | Net profit (₹ crore) | Employees | Headquarter |
|------|---------------------------|--------------|--------------------|-----------------------|-----------|--------------|
| 1    | Reliance Industries       | Conglomerate | 514217             | 39354                 | 236334    | Mumbai       |
| 2    | Indian Oil Corporation    | Oil and gas  | 484362             | 22190                 | 312996    | New Delhi    |
| 3    | State Bank of India       | Banking      | 401448             | 22594                 | 245642    | Mumbai       |
| ...  | ...                       | ...          | ...                | ...                   | ...       | ...          |

---

## ✅ Prerequisites

```bash
pip install beautifulsoup4 requests pandas
```

---

## 💡 Use Cases

- Exploratory Data Analysis (EDA)
- Business research
- Data visualization projects
- Automation of web data extraction

---

## 📜 License

This project is for educational purposes and uses publicly available data from Wikipedia.
