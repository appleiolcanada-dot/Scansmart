# Data Sources & APIs

This document provides comprehensive information about all data sources used by Scansmart, including how to obtain API keys, rate limits, costs, and integration details.

## Overview

Scansmart integrates data from multiple sources to provide comprehensive intelligence:
- **Market Data**: Prices, volumes, fundamentals
- **News**: Financial news from multiple publishers
- **Social Media**: Sentiment from Twitter, Reddit, etc.
- **Government**: SEC filings, FDA approvals
- **Economic**: Macro indicators, interest rates

## Market Data Sources

### 1. Alpha Vantage

**Purpose**: Stock prices, fundamentals, technical indicators

**Website**: https://www.alphavantage.co

**Pricing**:
- Free: 5 API calls/minute, 500/day
- Premium: Starting at $49.99/month (75 calls/minute)

**Data Coverage**:
- Real-time and historical stock prices (US markets)
- Fundamental data (income statement, balance sheet, cash flow)
- Technical indicators (pre-calculated)
- Forex, crypto, commodities

**Rate Limits**:
- Free: 5 calls/minute, 500/day
- Premium: 75-1200 calls/minute depending on tier

**API Key**: 
1. Visit https://www.alphavantage.co/support/#api-key
2. Enter email
3. Receive key instantly

**Integration Priority**: Primary (Free tier good for starting)

**Scansmart Usage**:
- Daily price updates
- Fundamental data refresh
- Technical indicator calculations

**Example Endpoint**:
```
https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=AAPL&apikey=YOUR_KEY
```

---

### 2. Polygon.io

**Purpose**: Real-time market data, options, forex, crypto

**Website**: https://polygon.io

**Pricing**:
- Free: 5 API calls/minute (stocks only)
- Starter: $29/month (real-time US stocks)
- Developer: $99/month (real-time + options)
- Advanced: $299-699/month (websockets, unlimited)

**Data Coverage**:
- Real-time stock prices (all US exchanges)
- Historical data (tick-level available)
- Options data
- Forex and crypto
- Company information

**Rate Limits**:
- Free: 5 calls/minute
- Paid: Varies by tier (up to unlimited)

**API Key**:
1. Sign up at https://polygon.io
2. Verify email
3. API key in dashboard

**Integration Priority**: Secondary (Better for real-time if budget allows)

**Scansmart Usage**:
- Intraday price updates
- Real-time streaming (WebSocket)
- Options data analysis

**Example Endpoint**:
```
https://api.polygon.io/v2/aggs/ticker/AAPL/range/1/day/2023-01-01/2023-12-31?apiKey=YOUR_KEY
```

---

### 3. Yahoo Finance (Unofficial)

**Purpose**: Backup market data source

**Website**: https://finance.yahoo.com

**Pricing**: Free (unofficial API, no official support)

**Data Coverage**:
- Real-time quotes (15-minute delay for free)
- Historical prices
- Basic fundamentals
- Options chains
- Company profiles

**Rate Limits**: Unofficial, be respectful (max 2000 requests/hour recommended)

**API Key**: Not required

**Integration Priority**: Tertiary (Backup when primary sources fail)

**Python Library**: `yfinance`
```python
import yfinance as yf
data = yf.download('AAPL', start='2023-01-01', end='2023-12-31')
```

**Scansmart Usage**:
- Fallback data source
- Quick validation
- Free tier users

---

### 4. Financial Modeling Prep

**Purpose**: Comprehensive fundamental data

**Website**: https://financialmodelingprep.com

**Pricing**:
- Free: 250 requests/day
- Starter: $14/month (300 requests/day)
- Professional: $29/month (500 requests/day)
- Enterprise: Custom

**Data Coverage**:
- Financial statements (10+ years history)
- Key metrics and ratios
- Company profiles and ratings
- Insider trading
- ETF holdings
- Economic indicators

**Rate Limits**: Based on tier (250-500+ per day)

**API Key**:
1. Sign up at https://financialmodelingprep.com/developer
2. Get API key from dashboard

**Integration Priority**: Primary for fundamentals

**Scansmart Usage**:
- Fundamental screening
- Company profiles
- Insider tracking

**Example Endpoint**:
```
https://financialmodelingprep.com/api/v3/income-statement/AAPL?apikey=YOUR_KEY
```

---

## News Sources

### 5. NewsAPI

**Purpose**: News aggregation from 80,000+ sources

**Website**: https://newsapi.org

**Pricing**:
- Free: 100 requests/day, 1 month history
- Developer: $449/month, unlimited requests, full archive

**Data Coverage**:
- 80,000+ news sources
- Business, financial news
- Multiple languages
- Search by keyword, source, date

**Rate Limits**:
- Free: 100 requests/day
- Paid: Unlimited

**API Key**:
1. Register at https://newsapi.org/register
2. Get key instantly

**Integration Priority**: Primary for news

**Scansmart Usage**:
- News feed
- Sentiment analysis input
- Catalyst detection from news

**Example Endpoint**:
```
https://newsapi.org/v2/everything?q=Apple&apiKey=YOUR_KEY
```

---

### 6. Finnhub

**Purpose**: Financial news and market data

**Website**: https://finnhub.io

**Pricing**:
- Free: 60 API calls/minute
- Starter: $49/month (300 calls/minute)
- Growth: $149/month (600 calls/minute)
- Enterprise: Custom

**Data Coverage**:
- Real-time news
- Company news
- Press releases
- Market news
- Economic calendar
- Earnings calendar

**Rate Limits**:
- Free: 60 calls/minute
- Paid: 300-600+ calls/minute

**API Key**:
1. Sign up at https://finnhub.io/register
2. Get API key from dashboard

**Integration Priority**: Primary for news and events

**Scansmart Usage**:
- News aggregation
- Earnings calendar
- Economic events

**Example Endpoint**:
```
https://finnhub.io/api/v1/company-news?symbol=AAPL&from=2023-01-01&to=2023-12-31&token=YOUR_KEY
```

---

## Social Media Sources

### 7. Twitter API v2

**Purpose**: Social sentiment analysis

**Website**: https://developer.twitter.com

**Pricing**:
- Free: Very limited (1,500 tweets/month)
- Basic: $100/month (10,000 tweets/month)
- Pro: $5,000/month (1M tweets/month)
- Enterprise: Custom

**Data Coverage**:
- Recent tweets (7 days for free/basic)
- Tweet search
- User data
- Engagement metrics

**Rate Limits**: Based on tier

**API Key**:
1. Apply for developer account at https://developer.twitter.com
2. Create project and app
3. Get Bearer Token

**Integration Priority**: Secondary (expensive for comprehensive data)

**Scansmart Usage**:
- Social sentiment
- Trending stocks
- Retail trader sentiment

**Note**: Consider Reddit as alternative (better signal for stocks)

---

### 8. Reddit API

**Purpose**: Community sentiment (WallStreetBets, stocks, investing)

**Website**: https://www.reddit.com/dev/api

**Pricing**: Free (rate limited)

**Data Coverage**:
- Subreddit posts and comments
- Upvotes/downvotes
- User data
- Real-time streams

**Rate Limits**: 60 requests/minute

**API Key**:
1. Go to https://www.reddit.com/prefs/apps
2. Create app (script type)
3. Get client_id and client_secret

**Integration Priority**: Primary for social sentiment

**Scansmart Usage**:
- WallStreetBets sentiment
- Retail trader trends
- Discussion analysis

**Python Library**: `praw`
```python
import praw
reddit = praw.Reddit(client_id='YOUR_ID', client_secret='YOUR_SECRET', user_agent='Scansmart')
```

---

## Government & Regulatory Sources

### 9. SEC EDGAR

**Purpose**: SEC filings (official)

**Website**: https://www.sec.gov/edgar

**Pricing**: Free

**Data Coverage**:
- 10-K, 10-Q (annual, quarterly reports)
- 8-K (current events)
- Form 4 (insider trading)
- Proxy statements
- All public company filings

**Rate Limits**: 10 requests/second (enforced)

**API Key**: Not required

**Integration Priority**: Primary (official source)

**Scansmart Usage**:
- Catalyst detection (8-K filings)
- Insider trading tracking (Form 4)
- Fundamental analysis (10-K/Q)

**API Endpoint**:
```
https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=AAPL&type=&dateb=&owner=include&count=100
```

**Best Practice**: Include User-Agent header with contact info

---

### 10. FDA API

**Purpose**: Drug approvals, clinical trials

**Website**: https://open.fda.gov

**Pricing**: Free

**Data Coverage**:
- Drug approvals and applications
- Enforcement reports
- Adverse events
- Clinical trials (ClinicalTrials.gov)

**Rate Limits**: 
- No key: 240 requests/minute, 120,000/day
- With key: 240 requests/minute, no daily limit

**API Key**:
1. Sign up at https://open.fda.gov/apis/authentication/
2. Get API key

**Integration Priority**: Primary for biotech catalysts

**Scansmart Usage**:
- FDA approval calendar
- Clinical trial tracking
- Biotech catalyst detection

**Example Endpoint**:
```
https://api.fda.gov/drug/event.json?search=patient.drug.openfda.brand_name:lipitor&limit=1
```

---

## Economic Data Sources

### 11. FRED (Federal Reserve)

**Purpose**: Economic indicators

**Website**: https://fred.stlouisfed.org

**Pricing**: Free

**Data Coverage**:
- GDP, unemployment, inflation
- Interest rates
- Manufacturing indices
- Consumer confidence
- 816,000+ time series

**Rate Limits**: Not strictly enforced

**API Key**:
1. Register at https://fred.stlouisfed.org/docs/api/api_key.html
2. Get API key

**Integration Priority**: Secondary (for macro context)

**Scansmart Usage**:
- Market conditions context
- Sector rotation signals
- Risk-on/risk-off indicators

---

## Alternative Data Sources

### 12. Quandl (Nasdaq Data Link)

**Purpose**: Alternative and financial data

**Website**: https://data.nasdaq.com

**Pricing**:
- Free: Limited datasets
- Premium: $50-1000+/month per dataset

**Data Coverage**:
- Financial data
- Alternative data
- Economic data
- Commodities

**Integration Priority**: Optional (expensive)

---

### 13. USPTO (Patent Data)

**Purpose**: Patent filings and grants

**Website**: https://www.uspto.gov

**Pricing**: Free

**Data Coverage**:
- Patent applications
- Patent grants
- Trademark data

**Integration Priority**: Tertiary (niche use case)

**Scansmart Usage**:
- Technology company catalysts
- Innovation tracking

---

## Data Integration Strategy

### Primary Stack (MVP)
1. **Market Data**: Alpha Vantage (free tier)
2. **News**: NewsAPI (free tier) + Finnhub (free tier)
3. **Social**: Reddit API (free)
4. **Filings**: SEC EDGAR (free)
5. **Biotech**: FDA API (free)

**Total Cost**: $0/month

### Recommended Stack (Production)
1. **Market Data**: Polygon.io ($99/month) + Alpha Vantage backup
2. **News**: Finnhub Pro ($149/month)
3. **Social**: Reddit API (free)
4. **Filings**: SEC EDGAR (free)
5. **Biotech**: FDA API (free)
6. **Fundamentals**: Financial Modeling Prep ($29/month)

**Total Cost**: ~$277/month

### Enterprise Stack (Scale)
1. **Market Data**: Polygon Advanced ($699/month)
2. **News**: NewsAPI Developer ($449/month)
3. **Social**: Twitter Pro ($5,000/month) + Reddit
4. **Filings**: SEC EDGAR (free)
5. **Biotech**: FDA API (free)
6. **Fundamentals**: Multiple premium sources

**Total Cost**: $6,000+/month

---

## Rate Limiting Strategy

### Implementation
```python
from ratelimit import limits, sleep_and_retry

@sleep_and_retry
@limits(calls=5, period=60)  # 5 calls per minute
def call_alpha_vantage_api():
    # API call here
    pass
```

### Caching
- Cache responses for appropriate duration
- Market data: 1 minute (intraday), 1 hour (daily)
- News: 5 minutes
- Fundamentals: 1 day
- Filings: 1 hour

### Fallback Strategy
1. Try primary source
2. Check cache
3. Try secondary source
4. Return cached data (even if stale)
5. Log error for investigation

---

## Cost Optimization Tips

1. **Use Free Tiers First**: Start with free APIs, upgrade only when necessary
2. **Batch Requests**: Combine multiple requests when possible
3. **Smart Caching**: Cache aggressively to reduce API calls
4. **Rate Limit Efficiently**: Use full quota but don't waste calls
5. **Choose Right Source**: Use cheapest source that meets quality needs
6. **Monitor Usage**: Track API usage to avoid surprise bills
7. **Negotiate**: For high volume, negotiate custom pricing
8. **User-Funded**: Pass costs to users (e.g., BYO API keys)

---

## Data Quality Considerations

### Validation
- Cross-check data from multiple sources
- Detect anomalies (e.g., price spikes)
- Handle missing data gracefully
- Log data quality issues

### Freshness
- Monitor data lag
- Alert on stale data
- Display data timestamps to user
- Clearly mark delayed data

### Reliability
- Monitor API uptime
- Have backup data sources
- Implement circuit breakers
- Graceful degradation

---

## Legal & Compliance

### Terms of Service
- Read and comply with each API's ToS
- Don't exceed rate limits
- Don't resell raw data (usually prohibited)
- Attribute data sources where required

### Data Rights
- Most financial data APIs allow derived works
- Cannot redistribute raw data
- AI training may have restrictions
- Check each provider's policy

### User Data
- Store API keys securely (encrypted)
- Don't expose keys in frontend
- Rotate keys periodically
- Limit key permissions

---

## Monitoring & Alerts

### Metrics to Track
- API call volume per source
- Success/error rates
- Response times
- Cost per API call
- Cache hit rates

### Alerts
- API quota approaching limit (80%)
- High error rates (>5%)
- Slow response times (>2 seconds)
- API downtime
- Unexpected costs

### Dashboard
- Real-time API usage
- Cost tracking
- Error logs
- Performance metrics

---

## Future Data Sources

### Under Consideration
- **Bloomberg API**: Too expensive, but comprehensive
- **Refinitiv**: High quality, institutional pricing
- **Alternative Data**: Web scraping, satellite imagery, credit card data
- **Options Flow**: Unusual options activity detection
- **Dark Pool**: Institutional trading data
- **Short Interest**: Borrow rates and availability

### Community Data
- User-submitted catalysts
- Crowdsourced earnings estimates
- Community ratings and sentiment

---

## Getting Started Checklist

- [ ] Sign up for Alpha Vantage (free)
- [ ] Sign up for NewsAPI (free)
- [ ] Create Reddit app
- [ ] Read SEC EDGAR API docs
- [ ] Sign up for FDA API key
- [ ] Sign up for Finnhub (free)
- [ ] Add all keys to `.env` file
- [ ] Test each API with sample requests
- [ ] Set up rate limiting
- [ ] Configure caching
- [ ] Set up monitoring

---

## Resources

- **API Testing**: Postman, Insomnia
- **Rate Limiting**: `ratelimit` (Python), `bottleneck` (Node.js)
- **Caching**: Redis, Memcached
- **Monitoring**: Prometheus, Grafana, Datadog
- **Documentation**: Each provider's official docs

---

## Support

For issues with specific APIs:
- Check provider's documentation
- Check status page (most providers have one)
- Contact provider support
- Search provider's community forum

For Scansmart integration issues:
- Check [GitHub Issues](https://github.com/appleiolcanada-dot/Scansmart/issues)
- Review integration code in `backend/app/integrations/`
- Test API endpoints directly first
