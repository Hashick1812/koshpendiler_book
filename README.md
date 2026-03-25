# 📚 Lab Work 1 — NLP & Web Scraping Analysis

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![pdfplumber](https://img.shields.io/badge/pdfplumber-PDF%20Parsing-lightgrey)
![Selenium](https://img.shields.io/badge/Selenium-Web%20Scraping-43B02A?logo=selenium&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

A two-part data science lab project combining **Natural Language Processing (NLP)** on a classic Kazakh literary trilogy with **real estate web scraping** from Kazakhstan's largest property platform.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Task 1 — Köshpendiler NLP Analysis](#task-1--köshpendiler-nlp-analysis)
- [Task 2 — Krisha.kz Web Scraping](#task-2--krishakz-web-scraping)
- [Datasets](#datasets)
- [Installation](#installation)
- [Usage](#usage)
- [Key Findings](#key-findings)
- [Technologies Used](#technologies-used)
- [References](#references)

---

## Overview

This lab is divided into two independent tasks:

| Task | Topic | Method |
|------|-------|--------|
| **Task 1** | NLP on *Köshpendiler* trilogy by Ilyas Esenberlin | PDF extraction, text cleaning, frequency analysis, visualisation |
| **Task 2** | Real estate listings from Krisha.kz | Selenium headless browser scraping, data cleaning, price analysis |

---

## Project Structure

```
📦 lab-work-1/
 ┣ 📓 lab_work_1_final_version.ipynb   # Main notebook (Task 1 + Task 2)
 ┣ 📓 Lab_Task_1.ipynb                 # Task 1 draft / prototype
 ┣ 📄 1.pdf                            # Köshpendiler Vol.1 — Алмас Қылыш
 ┣ 📄 2.pdf                            # Köshpendiler Vol.2 — Жанталас
 ┣ 📄 3.pdf                            # Köshpendiler Vol.3 — Қаһар
 ┣ 📊 koshpendiler_dataset.csv         # Extracted book text (book, page, text)
 ┣ 📊 koshpendiler_dataset.json        # Same dataset in JSON format
 ┣ 📄 koshpendiler_dataset.txt         # Plain text version of extracted pages
 ┣ 📊 krisha_10000.csv                 # 10,000 scraped apartment listings
 ┣ 📊 krisha_10000.xlsx                # Same data in Excel format
 ┗ 📄 README.md                        # This file
```

---

## Task 1 — Köshpendiler NLP Analysis

### Source Material
The analysis uses all three volumes of **Ілияс Есенберлин's** famous historical trilogy *Көшпенділер* (The Nomads):

| Volume | Kazakh Title | English Title |
|--------|-------------|---------------|
| Book 1 | Алмас Қылыш | Diamond Sword |
| Book 2 | Жанталас     | The Desperate Times |
| Book 3 | Қаһар        | Wrath |

### Pipeline

1. **PDF Extraction** — Text extracted from all 3 PDFs using `pdfplumber`
2. **Text Cleaning** — Hyphenation fixed, whitespace normalised, repeated headers removed
3. **Tokenisation** — Words and sentences split using Unicode-aware regex
4. **Stopword Filtering** — Custom Kazakh stopword list applied
5. **Analysis & Visualisation:**
   - Top-20 most frequent words (bar chart)
   - Sentence length distribution (histogram + KDE)
   - Vocabulary growth curve across the corpus
   - Unique word counts per volume (bar chart)
   - Keyword tracking — occurrences of `қазақ` across 3 books
   - Historical character mention frequency (Кенесары, Абылай, Наурызбай, etc.)
   - Punctuation usage analysis per book
   - Word cloud for the full corpus
   - Word length distribution

---

## Task 2 — Krisha.kz Web Scraping

### Target
**[krisha.kz](https://krisha.kz)** — Kazakhstan's largest real estate marketplace.

### Scraping Method
- Headless Chrome via **Selenium** + **WebDriver Manager**
- Scrolls each page 5× to trigger lazy-loaded listings
- Random delays (1–3 sec) between requests to avoid detection
- Scraped until **10,000+ listings** were collected

### Data Collected per Listing

| Field | Description |
|-------|-------------|
| `platform` | Source site (krisha) |
| `title` | Listing title (rooms, area) |
| `link` | Direct URL to listing |
| `price` | Raw price string |
| `location` | Address / district |
| `price_clean` | Parsed numeric price (KZT) |

### Analysis
- Price distribution histogram (KDE overlay)
- Top-10 most expensive listings
- Average price by district in Almaty
- Price distribution by region (top 8 regions, boxplot)
- Linear regression on price trend
- Room count extraction from titles

---

## Datasets

| File | Format | Rows | Description |
|------|--------|------|-------------|
| `koshpendiler_dataset.csv` | CSV | ~2,400 pages | Extracted book text, one row per page |
| `koshpendiler_dataset.json` | JSON | ~2,400 pages | Same data in JSON format |
| `koshpendiler_dataset.txt` | TXT | — | Plain text dump of all pages |
| `krisha_10000.csv` | CSV | 10,000 | Apartment listings with prices |
| `krisha_10000.xlsx` | Excel | 10,000 | Same as above |

---

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/lab-work-1.git
   cd lab-work-1
   ```

2. **Install dependencies**
   ```bash
   pip install pdfplumber pandas numpy matplotlib seaborn plotly wordcloud nltk tqdm scikit-learn selenium webdriver-manager openpyxl
   ```

3. **Download NLTK data** (first run only)
   ```python
   import nltk
   nltk.download('punkt')
   ```

4. **Open the notebook**
   ```bash
   jupyter notebook lab_work_1_final_version.ipynb
   ```

> ⚠️ **For Task 2 re-scraping:** Google Chrome must be installed. The notebook uses `webdriver-manager` to auto-download ChromeDriver. The scraping step can take 30–60 minutes for 10,000 listings. Pre-scraped data is already included in `krisha_10000.csv`.

---

## Usage

Run `lab_work_1_final_version.ipynb` section by section:

| Section | What it does |
|---------|-------------|
| **Task 1 — PDF extraction** | Loads all 3 PDFs, extracts page text |
| **Task 1 — Cleaning** | Cleans hyphenation, whitespace, duplicates |
| **Task 1 — Statistics** | Prints word/sentence counts per book |
| **Task 1 — Frequency analysis** | Top-20 words after stopword removal |
| **Task 1 — Visualisations** | All 8 charts |
| **Task 2 — Scraping** | Runs Selenium scraper (or loads CSV) |
| **Task 2 — Cleaning** | De-duplicates, parses prices |
| **Task 2 — Analysis** | Price distributions, region analysis, regression |

---

## Key Findings

### Task 1 — NLP
- 🗺️ The keyword **қазақ** (Kazakh) appears most frequently in Book 3, reflecting its climax of national themes
- ⚔️ **Кенесары** is the most-mentioned historical figure across all three books
- 📝 Average sentence length is **12–15 words**, consistent across all three volumes
- 📖 Vocabulary grows steadily — Books 2 and 3 introduce less new vocabulary than Book 1, suggesting stylistic consistency
- 🔤 Live-text passes (commas and periods) dominate punctuation, with exclamation marks spiking in dramatic chapters

### Task 2 — Real Estate
- 🏙️ Almaty listings dominate the dataset, with the highest average prices
- 💰 Price distribution is heavily right-skewed — most apartments cluster under 30M KZT with a long tail of luxury properties
- 📍 Central district locations (Алматы орталық) command significantly higher prices than outskirt regions
- 📉 Linear regression shows a slight upward price trend across listing index (time proxy)

---

## Technologies Used

| Library / Tool | Purpose |
|----------------|---------|
| `pdfplumber` | PDF text extraction |
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Static plots |
| `seaborn` | Statistical visualisations |
| `plotly` | Interactive charts |
| `wordcloud` | Word cloud generation |
| `nltk` | NLP tokenisation utilities |
| `scikit-learn` | Linear regression (price trends) |
| `selenium` | Headless browser scraping |
| `webdriver-manager` | Auto ChromeDriver management |
| `BeautifulSoup` | HTML parsing |
| `tqdm` | Progress bars |

---

## References

- **FBref data source (Task 1 source material):** Ілияс Есенберлин, *Көшпенділер* trilogy, © І. Есенберлин атындағы қор, 2004
- **Krisha.kz:** https://krisha.kz — Kazakhstan's real estate marketplace
- **pdfplumber documentation:** https://github.com/jsvine/pdfplumber
- **Selenium documentation:** https://selenium-python.readthedocs.io

---

## License

This project is open-source and available under the [MIT License](LICENSE).
