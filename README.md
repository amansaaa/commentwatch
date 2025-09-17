# Setup

## Prerequisites
- Python 3.9.7
- PostgreSQL 14+

## Installation

# Purpose

Build a machine learning pipeline that turns consumer comments from different industries on social media (beauty, entertainment, & streetwear) into intraday signals for assets tied to those sectors

# Details

- Sectors: Sneakers/Footwear/Streetwear, Entertainment (Film, TV/Streaming), Beatuy/Skin Care

- Intraday horizons: 5m, 30m, 60m

- Platform: Reddit (free API usage)

- Demand signals: comments (volume, velocity, acceleration), purchase intent rate, engagement, stance, novelty (new info/opinions vs. repetitive statements), dispersion (spread of opinion)

# Repo Structure 

```
commentwatch/
├── config/
│   ├── subs.yaml                           # per-sector subreddit lists
│   ├── tickers.yaml                        # brand→ticker map (with synonyms, parent)
│   └── lexicon/
│       ├── purchase_intent.yml             # PIR+/- phrases (regex)
│       └── finance_terms.yml               # optional co-occurrence guard words
├── ingestion/
│   ├── reddit_client.py                    # OAuth client (no scraping)
│   └── scheduler.py                        # clock-driven polling
├── processing/
│   ├── clean.py                            # text cleaning + language ID + dedup
│   ├── map_tickers.py                      # dictionary + rules → mentions
│   ├── features.py                         # rolling bar aggregation
│   ├── embeddings.py                       # novelty (later)
│   └── stance_model.py                     # simple stance classifier (later)
├── marketdata/
│   ├── bars.py                             # 1-5m OHLCV loader
│   └── align.py                            # freeze logic + session alignment
├── backtest/
│   ├── targets.py                          # return targets
│   ├── simulator.py                        # walk-forward, costs, sizing
│   └── metrics.py                          # IC, Sharpe, p@k
├── dashboard/
│   └── app.py                              # Streamlit research view
├── storage/
│   ├── schema.sql                          # Postgres DDL
│   └── db.py                               # thin insert/select helpers
├── notebooks/
│   └── dev_exploration.ipynb
├── data/
│   └── raw/                                # raw JSON payloads (gitignored)
├── .env.example                            # secrets template (do not commit .env)
├── requirements.txt                        # Python dependencies
└── README.md
```
