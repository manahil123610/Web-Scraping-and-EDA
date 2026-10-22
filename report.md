# Lab 02 Report: Web Scraping, Feature Engineering and EDA

**Name:** Manahil Rasool  **SAP ID:** 70177665  **Course:** AI-101L

## 1. NumPy vs native Python loop (Task 2.1)

| Method | Time (sec) |
|---|---|
| NumPy `np.sum` (10,000,000 values) | **TODO: paste from your Colab run** |
| Python `for` loop | **TODO: paste from your Colab run** |
| Speed-up | **TODO: paste "NumPy is Nx faster"** |

The sums agree, but the loop is orders of magnitude slower. NumPy runs the loop inside compiled C code, while the Python loop executes ten million interpreted iterations.

## 2. Data acquisition (Task 2.2)

Five blog URLs from techncruncher.blogspot.com were targeted. **Four** were scraped successfully and cached in `articles_raw.csv`. The fifth (the CJ Affiliate guide) is absent from the cache.

**Exercise 1: why the selectors failed.** **TODO:** open the missing page, right-click the body text and Inspect, then state the tag and class actually used compared with `div.post-body.entry-content`. Add your two extra URLs and say which failed and why.

## 3. Feature engineering (Task 2.3)

Features per article (full table in `articles.csv`):

| Article | Tokens | Sentences | Entities | Nouns | Verbs | Avg sent. len | Polarity | Subjectivity |
|---|---|---|---|---|---|---|---|---|
| Top 10 AI Tools 2025 | 1188 | 47 | 24 | 321 | 150 | 25.3 | 0.229 | 0.584 |
| LimeWire AI Studio Review | 1723 | 65 | 103 | 420 | 200 | 26.5 | 0.219 | 0.574 |
| Top 10 AI Tools 2023 | 1480 | 52 | 39 | 331 | 166 | 28.5 | 0.197 | 0.436 |
| Top 10 AI Content Generators 2022 | 1319 | 63 | 89 | 271 | 140 | 20.9 | 0.215 | 0.565 |

## 4. EDA findings (Task 2.4)

Figures are in `figures/`.

- **Sentiment:** all four articles are mildly positive (polarity 0.20 to 0.23) and fairly subjective (0.44 to 0.58). This fits promotional blog writing: opinion that something is good, not evidence that it is.
- **Polarity histogram:** the values are tightly clustered, so there is almost no spread to describe. With n = 4, the bars and KDE curve show where the points are, not a distribution.
- **Pair plot and correlations:** `num_sentences` and `num_entities` correlate at 1.00, and `num_tokens` and `num_verbs` at 0.92. Longer articles simply contain more of everything. With n = 4, these coefficients are indicative only and a single article can swing them.
- **LimeWire article:** it has by far the most entities (103), because it names many platforms, coins, artists and models. The 2025 article, which describes tools rather than people and organisations, has only 24.

## 5. TF-IDF interpretation

- **With `stop_words='english'`** the top terms are content-bearing: *content, ai, tool, month, limewire, creators, tools, plan, features...*, which describe the topic of these articles (AI tools, pricing plans, creators).
- **With `stop_words=None`** the list is dominated by function words: *and, the, to, for, it, of, you, is, in, with, that, as, can, your*. Fourteen of the top 20 terms are stop words.
- **Why:** stop words occur in every document, so IDF should push them down, but with only four documents there is little room for IDF to discriminate, and their high term frequency dominates. Removing them is what makes the term list informative.

## 6. Exercise 3: KDE over five points

A kernel density estimate places a smooth curve over each data point and sums them. With five points, the shape is determined mostly by the chosen bandwidth and by where those few points happen to fall, not by the underlying population. It would suggest a smooth, continuous distribution that five samples cannot support, and one extra article could change its shape completely. Instead, I would report the raw values (a strip plot or the table), the mean and range, and label any plot as "n = 5, descriptive only". To describe a population, I would collect many more articles (tens at minimum) and report confidence intervals or a bootstrap estimate of the mean.

## 7. Home assignment (two blogs, 20 articles)

**TODO:** run the scraper on two blogs (10 URLs each), then fill in:

| Source | n | Mean polarity | Mean noun density |
|---|---|---|---|
| Blog A | | | |
| Blog B | | | |
| Difference | | | |

Noun density = `num_nouns / num_tokens`. Include the grouped bar chart (`figures/home_assignment_bar.png`).

**Sample-size paragraph (TODO):** state whether the difference is meaningful. With 10 articles per blog, the standard error of each mean is large relative to likely differences, and articles within a blog are not independent samples of "the blog's style". A difference of this size should be treated as suggestive, and a t-test p-value or confidence interval should be reported alongside the means.
