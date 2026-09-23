# NLP Project on r/Linguistics Subreddit

A reproducible Jupyter Notebook workflow for collecting and analyzing Reddit discussions about minority languages, language endangerment, language shift, language maintenance, and related topics in `r/linguistics`.

## Overview

The project uses the Reddit API to gather posts and comments matching a set of topic queries, then applies natural language processing and exploratory analysis techniques to the resulting corpus. The notebook currently demonstrates a dataset of approximately 30,000 Reddit posts and comments and identifies languages mentioned in the text.

The workflow includes:

- Reddit data collection through [PRAW](https://praw.readthedocs.io/)
- Data organization with pandas
- Text cleaning, lemmatization, tokenization, unigrams, and bigrams
- Language-name matching using [pycountry](https://github.com/flyingcircusio/pycountry)
- BERT tokenization with `bert-base-uncased`
- NLP and topic-modeling utilities from Gensim and scikit-learn
- Visualizations including word clouds, Matplotlib, Seaborn, Plotly, and pyLDAvis

## Repository contents

```text
.
└── Digital Methods Code.ipynb    # End-to-end data collection and NLP analysis notebook
```

## Requirements

- Python 3.11 recommended
- Jupyter Notebook or JupyterLab
- A Reddit API application with valid credentials
- Python packages used by the notebook, including:
  - `praw`
  - `pandas`
  - `numpy`
  - `nltk`
  - `transformers`
  - `gensim`
  - `scikit-learn`
  - `pycountry`
  - `matplotlib`
  - `seaborn`
  - `plotly`
  - `wordcloud`
  - `tqdm`
  - `pyLDAvis`

Because the repository does not currently include a pinned dependency file, installing packages as needed from the notebook may be necessary.

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/NadireWaili/NLP-Project-on-r-Linguistics-Subreddit.git
cd NLP-Project-on-r-Linguistics-Subreddit
```

### 2. Create an environment

```bash
python -m venv .venv
source .venv/bin/activate        # macOS/Linux
# .venv\\Scripts\\activate     # Windows PowerShell

python -m pip install --upgrade pip
python -m pip install jupyter praw pandas numpy nltk transformers gensim scikit-learn pycountry matplotlib seaborn plotly wordcloud tqdm pyLDAvis chart-studio
```

### 3. Configure Reddit API access

Create a Reddit application at <https://www.reddit.com/prefs/apps> and configure PRAW using environment variables or another secure secret-management method:

```bash
export REDDIT_CLIENT_ID="your-client-id"
export REDDIT_CLIENT_SECRET="your-client-secret"
export REDDIT_USER_AGENT="linguistics-nlp-project/1.0 by your-reddit-username"
```

Do not commit Reddit client secrets to the notebook or repository. Before running the notebook, update the PRAW initialization to read these environment variables.

### 4. Launch the notebook

```bash
jupyter notebook "Digital Methods Code.ipynb"
```

Run the cells from top to bottom. The notebook downloads required NLTK resources, queries `r/linguistics`, builds a pandas DataFrame, preprocesses the text, detects language mentions, and generates visualizations.

## Analysis workflow

1. **Collect Reddit data** — searches `r/linguistics` for terms such as `minority language`, `endangerment`, `language shift`, `maintenance`, and `marginalized`, including post metadata and comment threads.
2. **Build the corpus** — combines post titles and text into `Text_all` and stores identifiers, scores, timestamps, URLs, parent IDs, and author IDs.
3. **Preprocess text** — the `Preprocessor` class lowercases text, removes numbers, whitespace, stopwords, punctuation, and selected meaningless tokens, then applies POS-aware lemmatization and tokenization.
4. **Identify languages** — compares tokenized text with language names from `pycountry` and records unique language mentions.
5. **Explore the results** — produces language word clouds and provides imports and utilities for frequency analysis, dimensionality reduction, topic modeling, and interactive topic visualization.

## Outputs

The notebook writes the collected Reddit corpus to a CSV file named `Linguistics.csv` in the working directory when the export cell is run. Some original notebook cells also reference local paths for exported CSV and image files; update those paths for your environment before running them.

## Notes and limitations

- Reddit search results and available comments can change over time, so rerunning the notebook may not reproduce the exact same dataset.
- The notebook may require NLTK resources such as stopwords, tokenizers, WordNet, POS taggers, and the averaged perceptron tagger. Download missing resources with `nltk.download(...)` when prompted.
- Exact language-name matching can produce false positives for short or ambiguous names, so detected languages should be reviewed before drawing conclusions.
- The collection and analysis process may be time-consuming because it retrieves complete comment trees with `replace_more(limit=None)`.
- Respect Reddit's API terms, rate limits, and the privacy of Reddit users when using or extending this project.

## Citation and data provenance

This project analyzes publicly available Reddit content from `r/linguistics`. If you reuse the analysis or derived results, cite this repository and follow Reddit's terms and applicable data-protection requirements.

## License

No license is currently included. Unless a license is added, standard copyright applies and reuse should be requested from the repository owner.
