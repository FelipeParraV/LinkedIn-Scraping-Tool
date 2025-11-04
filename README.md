# 🚀 LinkedIn Job Scraper

This project contains a Python script designed to scrape job posting data from **LinkedIn Jobs** based on a specified job title and location. It utilizes the `requests` library for fetching web content and `BeautifulSoup` for parsing the HTML. The results are compiled into a pandas DataFrame and saved to a CSV file.

---

## 🎯 Project Goal

The primary objective is to automate the collection of key job metrics (Title, Company, Experience Level, etc.) for a specific job search on LinkedIn, helping users quickly gather and analyze job market data.

---

## ⚙️ Prerequisites

To run this notebook, you'll need **Python 3** installed, along with the following libraries:

* **`requests`**: For making HTTP requests to LinkedIn.
* **`BeautifulSoup` (`bs4`)**: For parsing HTML content.
* **`pandas`**: For data manipulation and saving the results to a DataFrame/CSV.

You can install the required libraries using pip:

```bash
pip install requests beautifulsoup4 pandas
```
## 📝 Easy Usage

### 1. Configure Search Parameters

The search is configured in the second code cell of the notebook. Modify the following variables to change the search criteria:

* **`title`**: The job title you're searching for (e.g., `"Analyst"`). *Note: The script prepends `"data%20"` to your title in the URL, searching for `data [Your Title]`.*
* **`location`**: The geographical location for the search (e.g., `"Chile"`).
* **`size`**: The number of pages to scrape. Since each page loads **10 jobs**, setting `size = 10` attempts to scrape up to 100 job IDs.

### 2. Run the Notebook

Execute all cells in the `LinkedIn_Scraper.ipynb` notebook sequentially:

1.  **Import Libraries**
2.  **Define Search Parameters**
3.  **Scrape Job IDs**: Collects the unique ID for each job post across the specified number of pages.
4.  **Scrape Job Details**: Iterates through the collected IDs, visits each job's page, and extracts details (status codes of `429` indicate rate limiting).
5.  **Create DataFrame**: Converts the collected data into a pandas DataFrame.
6.  **Save to CSV**: The final cell saves the collected data.

### 3. Output

The script saves the collected data into a file named **`jobs.csv`** in the same directory as the notebook.

## 🗂️ Scraped Data Fields

The script collects the following data for each job:

| Field | Description |
| :--- | :--- |
| `job_title` | The name of the job posting. |
| `company_name` | The name of the hiring company. |
| `experience_level` | The required experience (e.g., Entry level, Associate). |
| `type_of_contract` | The employment type (e.g., Full-time, Contract). |
| `easy_apply` | Boolean: `True` if it's a LinkedIn Easy Apply job, `False` otherwise. |
| `time_posted` | How long ago the job was posted (e.g., 1 week ago). |
| `num_applicants` | The number of applicants shown on the post. |
| `job_link` | The direct URL to the job posting. |

## ⚠️ Troubleshooting: Rate Limiting

The scraper frequently encounters **`429 (Too Many Requests)`** errors. This means LinkedIn has temporarily rate-limited your requests.

* **Mitigation**: To improve the success rate, you should **introduce a time delay** (`time.sleep()`) within the job details scraping loop (Cell 4) to slow down consecutive requests.
