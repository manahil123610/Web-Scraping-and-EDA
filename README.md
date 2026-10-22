# Web-Scraping-and-EDA
End-to-end text analysis pipeline: scrape blog articles, engineer NLP features with spaCy and TextBlob, and explore them with EDA and TF-IDF.

## What it does

- **Scrapes** article titles and body text from blogs, with a browser-like User-Agent, timeouts and delays between requests
- **Engineers features** per article: token, sentence, noun, verb and named-entity counts, average sentence length, sentiment polarity and subjectivity
- **Explores** the features with distribution plots, a pair plot and correlation matrix
- **Ranks key terms** with TF-IDF and compares results with and without stop-word removal
- **Compares sources** by mean sentiment and noun density

## Findings

- The sample articles are mildly positive and fairly subjective, typical of promotional writing.
- Sentence and entity counts move together, since longer articles contain more of everything.
- Without stop-word removal, TF-IDF is dominated by words like "the" and "and"; with it, the top terms describe the actual topic.

## Files

| File | Contents |
|---|---|
| `scraping_eda.ipynb` | Full notebook with outputs |
| `articles_raw.csv` | Cached raw scrape |
| `articles.csv` | Corpus with engineered features |
| `figures/` | Plots |
| `report.md` | Detailed write-up |

## Tools

Python, pandas, requests, BeautifulSoup, spaCy, TextBlob, scikit-learn, matplotlib, seaborn.
