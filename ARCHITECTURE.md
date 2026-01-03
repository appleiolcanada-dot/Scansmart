# Scansmart Technical Architecture

## System Overview

Scansmart is built on a modern, scalable architecture optimized for single-user deployment while maintaining the capability to scale. The system is designed with modularity, performance, and intelligence at its core.

## Architecture Principles

1. **Modularity**: Each component is independent and can be developed/deployed separately
2. **Real-time First**: Built for streaming data and immediate insights
3. **AI-Native**: Intelligence integrated at every layer, not bolted on
4. **Single-User Optimized**: Resource efficient, can run on modest hardware
5. **Privacy-Focused**: All processing can happen locally, no mandatory cloud dependencies

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           Client Layer                              │
│  ┌──────────────┐  ┌──────────────┐  ┌────────────────────────┐   │
│  │ Web App      │  │ Mobile PWA   │  │ CLI Tools              │   │
│  │ (React/Next) │  │ (React)      │  │ (Python/Node)          │   │
│  └──────────────┘  └──────────────┘  └────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
                                 │
                         [HTTPS/WSS]
                                 │
┌─────────────────────────────────────────────────────────────────────┐
│                         API Gateway Layer                           │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  FastAPI Server                                               │  │
│  │  - REST API Endpoints                                         │  │
│  │  - WebSocket Connections                                      │  │
│  │  - Authentication (JWT)                                       │  │
│  │  - Rate Limiting                                              │  │
│  │  - Request Validation                                         │  │
│  └──────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
                                 │
        ┌────────────────────────┼────────────────────────┐
        │                        │                        │
┌───────▼────────┐    ┌──────────▼────────┐    ┌────────▼────────┐
│ Business Logic │    │   AI/ML Engine    │    │ Data Management │
│     Layer      │    │      Layer        │    │      Layer      │
└────────────────┘    └───────────────────┘    └─────────────────┘
        │                        │                        │
        └────────────────────────┼────────────────────────┘
                                 │
┌─────────────────────────────────────────────────────────────────────┐
│                      Data Storage Layer                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │
│  │PostgreSQL│  │ MongoDB  │  │  Redis   │  │  File Storage    │   │
│  │(Relational│  │(Document)│  │ (Cache)  │  │  (Models/Logs)   │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
                                 │
┌─────────────────────────────────────────────────────────────────────┐
│                    External Integration Layer                       │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │
│  │ Market   │  │  News    │  │  Social  │  │  Government      │   │
│  │ Data APIs│  │  APIs    │  │  Media   │  │  Data (SEC/FDA)  │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

## Component Details

### 1. Client Layer

#### Web Application (Primary Interface)
**Technology**: React 18+ with Next.js 14+
**Key Features**:
- Server-Side Rendering (SSR) for fast initial load
- Static Site Generation (SSG) for public pages
- Real-time updates via WebSocket
- Responsive design (mobile-first)
- Progressive Web App (PWA) capabilities

**Directory Structure**:
```
frontend/
├── app/                    # Next.js app directory
│   ├── dashboard/         # Main dashboard
│   ├── screener/          # Screening interface
│   ├── catalysts/         # Catalyst feed
│   ├── portfolio/         # Portfolio management
│   └── research/          # Research hub
├── components/            # Reusable components
│   ├── ui/               # Base UI components
│   ├── charts/           # Chart components
│   ├── tables/           # Data tables
│   └── forms/            # Form components
├── lib/                  # Utilities
│   ├── api.ts           # API client
│   ├── websocket.ts     # WebSocket client
│   └── utils.ts         # Helper functions
├── hooks/                # Custom React hooks
├── stores/               # State management (Zustand)
└── styles/               # Global styles
```

#### Mobile PWA
- Same codebase as web app
- Optimized layouts for mobile
- Offline-first architecture
- Push notification support

#### CLI Tools
**Technology**: Python Click / Node.js Commander
**Use Cases**:
- Power users who prefer terminal
- Automation and scripting
- Server-side cron jobs
- Quick queries without opening browser

### 2. API Gateway Layer

#### FastAPI Server
**Why FastAPI?**
- Async/await support (high concurrency)
- Automatic API documentation (OpenAPI/Swagger)
- Type validation with Pydantic
- WebSocket support
- High performance (comparable to Node.js, Go)

**Directory Structure**:
```
backend/
├── app/
│   ├── api/
│   │   ├── v1/
│   │   │   ├── endpoints/
│   │   │   │   ├── stocks.py      # Stock endpoints
│   │   │   │   ├── catalysts.py   # Catalyst endpoints
│   │   │   │   ├── screening.py   # Screening endpoints
│   │   │   │   ├── alerts.py      # Alert endpoints
│   │   │   │   ├── portfolio.py   # Portfolio endpoints
│   │   │   │   └── insights.py    # AI insights endpoints
│   │   │   └── api.py            # API router
│   │   └── deps.py               # Dependencies
│   ├── core/
│   │   ├── config.py            # Configuration
│   │   ├── security.py          # Auth & security
│   │   └── events.py            # Startup/shutdown events
│   ├── models/                  # Database models
│   ├── schemas/                 # Pydantic schemas
│   ├── services/                # Business logic
│   ├── crud/                    # Database operations
│   └── main.py                  # Application entry
├── tests/                       # Test suite
└── requirements.txt            # Dependencies
```

**Key Endpoints**:
```python
# Screening
POST   /api/v1/screen/create       # Create screening query
GET    /api/v1/screen/{id}/results # Get results
POST   /api/v1/screen/backtest     # Backtest strategy

# Catalysts
GET    /api/v1/catalysts/active    # Active catalysts
GET    /api/v1/catalysts/calendar  # Upcoming catalysts
GET    /api/v1/catalysts/{id}      # Catalyst details
WS     /api/v1/catalysts/stream    # Real-time catalyst stream

# Stocks
GET    /api/v1/stocks/{ticker}     # Stock details
GET    /api/v1/stocks/{ticker}/score # Intelligence score
GET    /api/v1/stocks/{ticker}/catalysts # Stock catalysts
POST   /api/v1/stocks/batch        # Batch stock data

# Alerts
POST   /api/v1/alerts              # Create alert
GET    /api/v1/alerts              # List alerts
PATCH  /api/v1/alerts/{id}         # Update alert
DELETE /api/v1/alerts/{id}         # Delete alert

# Portfolio
GET    /api/v1/portfolio           # Get portfolio
POST   /api/v1/portfolio/position  # Add position
GET    /api/v1/portfolio/analysis  # Portfolio analysis

# Insights
GET    /api/v1/insights/daily      # Daily insights
GET    /api/v1/insights/opportunities # Top opportunities
GET    /api/v1/insights/personalized # Personalized suggestions

# User
POST   /api/v1/auth/login          # Login
POST   /api/v1/auth/register       # Register
GET    /api/v1/user/preferences    # Get preferences
PATCH  /api/v1/user/preferences    # Update preferences
```

### 3. Business Logic Layer

#### Screening Engine
**Location**: `backend/app/services/screening/`

**Components**:
```python
screening/
├── engine.py              # Main screening engine
├── filters/
│   ├── technical.py      # Technical filters
│   ├── fundamental.py    # Fundamental filters
│   ├── catalyst.py       # Catalyst filters
│   └── composite.py      # Combined filters
├── scoring/
│   ├── scorer.py         # Scoring engine
│   ├── weights.py        # Score weights
│   └── normalizer.py     # Score normalization
├── backtester.py         # Backtesting engine
└── optimizer.py          # Parameter optimization
```

**Screening Flow**:
1. Parse user query/criteria
2. Apply filters in parallel where possible
3. Calculate composite scores
4. Rank by score
5. Apply user preferences
6. Return top N results

#### Catalyst Detection System
**Location**: `backend/app/services/catalysts/`

**Components**:
```python
catalysts/
├── detector.py           # Main catalyst detector
├── sources/
│   ├── news.py          # News aggregation
│   ├── sec.py           # SEC filing parser
│   ├── social.py        # Social media monitor
│   └── earnings.py      # Earnings calendar
├── classifier.py         # Catalyst classification
├── impact_scorer.py      # Impact prediction
└── timeline.py          # Catalyst timeline
```

**Detection Pipeline**:
1. Continuous data ingestion from sources
2. NLP processing and entity extraction
3. Catalyst type classification
4. Impact score prediction
5. Deduplication and aggregation
6. Storage and indexing
7. Real-time broadcast via WebSocket

### 4. AI/ML Engine Layer

#### Core ML Infrastructure
**Location**: `backend/app/ml/`

**Directory Structure**:
```python
ml/
├── models/
│   ├── sentiment/
│   │   ├── news_sentiment.py      # News sentiment model
│   │   └── social_sentiment.py    # Social sentiment model
│   ├── prediction/
│   │   ├── catalyst_impact.py     # Catalyst impact predictor
│   │   └── price_forecast.py      # Price movement predictor
│   ├── classification/
│   │   ├── event_classifier.py    # Event classification
│   │   └── pattern_recognizer.py  # Pattern recognition
│   └── recommendation/
│       └── personalization.py     # Personalization engine
├── training/
│   ├── data_preparation.py        # Data preprocessing
│   ├── train.py                   # Training scripts
│   └── evaluate.py                # Model evaluation
├── inference/
│   ├── predictor.py              # Inference engine
│   └── batch.py                  # Batch predictions
└── utils/
    ├── features.py               # Feature engineering
    └── evaluation.py             # Metrics
```

#### Model Details

##### 1. News Sentiment Model
**Type**: Fine-tuned Transformer (FinBERT or similar)
**Input**: Financial news article text
**Output**: Sentiment score (-1 to +1) + confidence
**Training Data**: Financial news with labeled sentiment
**Update Frequency**: Monthly retraining

##### 2. Catalyst Impact Predictor
**Type**: Gradient Boosting (XGBoost/LightGBM)
**Input**: 
- Catalyst type
- Company features (market cap, sector, volatility)
- Historical catalyst performance
- Market conditions
**Output**: Expected price impact (%) + probability
**Training Data**: Historical catalyst events with price outcomes
**Update Frequency**: Weekly retraining

##### 3. Event Classifier
**Type**: Multi-label Transformer
**Input**: Event description text
**Output**: Event type probabilities (earnings, FDA, M&A, etc.)
**Training Data**: Labeled historical events
**Update Frequency**: Monthly

##### 4. Pattern Recognizer
**Type**: Recurrent Neural Network (LSTM/GRU)
**Input**: Time series price/volume data + catalyst events
**Output**: Pattern identification and confidence
**Training Data**: Historical patterns with outcomes
**Update Frequency**: Weekly

##### 5. Personalization Engine
**Type**: Collaborative Filtering + Reinforcement Learning
**Input**: User actions, preferences, trading history
**Output**: Personalized opportunity rankings
**Training Data**: User interaction history
**Update Frequency**: Real-time online learning

#### Feature Store
**Technology**: Feast or custom solution
**Purpose**: Centralized feature management
**Features**:
- Online features (low-latency serving)
- Offline features (training)
- Point-in-time correctness
- Feature versioning

### 5. Data Management Layer

#### Data Ingestion Pipeline
**Location**: `backend/app/services/data/`

**Components**:
```python
data/
├── ingestion/
│   ├── market_data.py        # Market data ingestion
│   ├── news_data.py          # News ingestion
│   ├── sec_data.py           # SEC filings
│   └── social_data.py        # Social media
├── processing/
│   ├── cleaner.py            # Data cleaning
│   ├── normalizer.py         # Data normalization
│   └── enricher.py           # Data enrichment
├── storage/
│   ├── db_writer.py          # Database writes
│   └── cache_writer.py       # Cache writes
└── scheduler.py              # Job scheduling
```

**Data Flow**:
```
Source APIs → Ingestion Service → Processing → Storage
                     ↓
              [Rate Limiting]
                     ↓
              [Data Validation]
                     ↓
              [Deduplication]
                     ↓
         [Write to Database + Cache]
```

#### Task Queue System
**Technology**: Celery + Redis
**Purpose**: Background job processing

**Task Types**:
- **Real-time**: Catalyst detection, price updates (high priority)
- **Scheduled**: Daily data refresh, model retraining (medium priority)
- **On-demand**: Backtesting, custom screens (low priority)

**Queue Configuration**:
```python
# celeryconfig.py
task_routes = {
    'app.tasks.catalysts.*': {'queue': 'high'},
    'app.tasks.data.*': {'queue': 'medium'},
    'app.tasks.backtest.*': {'queue': 'low'},
}

task_time_limits = {
    'app.tasks.catalysts.*': 10,      # 10 seconds
    'app.tasks.data.*': 300,          # 5 minutes
    'app.tasks.backtest.*': 3600,     # 1 hour
}
```

### 6. Data Storage Layer

#### PostgreSQL (Primary Database)
**Purpose**: Structured data with ACID guarantees

**Schema Organization**:
```sql
-- Core tables
users, user_preferences, user_sessions

-- Market data
stocks, prices_daily, prices_intraday, fundamentals

-- Catalyst system
catalysts, catalyst_types, catalyst_outcomes

-- Screening
screens, screen_results, screen_history

-- Alerts
alerts, alert_triggers, alert_history

-- Portfolio
portfolios, positions, transactions

-- Intelligence
scores, patterns, predictions

-- Audit
audit_logs, api_usage
```

**Optimization**:
- Indexes on frequently queried columns
- Partitioning on date columns (prices, catalysts)
- Materialized views for complex queries
- Connection pooling (PgBouncer)

#### TimescaleDB Extension
**Purpose**: Time-series data optimization
**Tables**: prices_*, catalyst_history, score_history
**Benefits**:
- Automatic partitioning by time
- Compression for old data
- Efficient time-based queries

#### MongoDB (Document Store)
**Purpose**: Unstructured/semi-structured data

**Collections**:
```javascript
// Raw news articles
news_articles {
  _id, url, title, content, source, 
  published_at, ticker_mentions, sentiment
}

// SEC filings
sec_filings {
  _id, ticker, filing_type, filing_date,
  document_text, extracted_sections, summary
}

// Social media posts
social_posts {
  _id, platform, author, content, timestamp,
  ticker_mentions, sentiment, engagement
}

// User activity logs
activity_logs {
  _id, user_id, action, context, timestamp
}

// ML model metadata
models {
  _id, model_type, version, metrics,
  training_date, artifacts_path
}
```

#### Redis (Caching & Real-time)
**Purpose**: High-speed cache and pub/sub

**Use Cases**:
1. **Cache Layer**:
   - Stock quotes (TTL: 1 minute)
   - Screen results (TTL: 5 minutes)
   - User sessions (TTL: 24 hours)
   - API rate limiting counters

2. **Pub/Sub**:
   - Real-time catalyst broadcasts
   - Price update streams
   - Alert notifications

3. **Task Queue**:
   - Celery broker
   - Result backend

**Key Patterns**:
```
# Cache keys
stock:{ticker}:quote
stock:{ticker}:score
screen:{screen_id}:results
user:{user_id}:preferences

# Pub/Sub channels
catalysts:active
prices:{ticker}
alerts:{user_id}

# Task queue
celery:task:{task_id}
```

#### File Storage
**Purpose**: Large files and ML artifacts

**Structure**:
```
storage/
├── models/              # Trained ML models
│   ├── sentiment/
│   ├── prediction/
│   └── classification/
├── data/               # Downloaded datasets
│   ├── sec_filings/
│   └── news_archives/
├── exports/            # User data exports
└── logs/              # Application logs
```

### 7. External Integration Layer

#### API Integration Architecture

**Pattern**: Adapter Pattern
**Location**: `backend/app/integrations/`

**Structure**:
```python
integrations/
├── base.py                    # Base adapter interface
├── market_data/
│   ├── alpha_vantage.py      # Alpha Vantage adapter
│   ├── polygon.py            # Polygon adapter
│   └── yahoo_finance.py      # Yahoo Finance adapter
├── news/
│   ├── newsapi.py            # NewsAPI adapter
│   └── finnhub.py            # Finnhub adapter
├── social/
│   ├── twitter.py            # Twitter adapter
│   └── reddit.py             # Reddit adapter
└── government/
    ├── sec_edgar.py          # SEC EDGAR adapter
    └── fda.py                # FDA adapter
```

**Base Adapter Interface**:
```python
class BaseAPIAdapter(ABC):
    def __init__(self, api_key: str):
        self.api_key = api_key
        self.rate_limiter = RateLimiter()
        self.cache = Cache()
    
    @abstractmethod
    async def fetch(self, **kwargs):
        """Fetch data from API"""
        pass
    
    def _handle_rate_limit(self):
        """Handle rate limiting"""
        pass
    
    def _cache_response(self, key, data):
        """Cache API response"""
        pass
```

#### Rate Limiting Strategy
- Per-source rate limiters
- Exponential backoff on errors
- Queue requests when approaching limits
- Graceful degradation

#### Data Source Priorities
1. **Primary**: Paid APIs with SLA
2. **Secondary**: Free APIs as backup
3. **Tertiary**: Scraping (last resort, with respect for robots.txt)

### 8. Deployment Architecture

#### Single-User Deployment (Docker Compose)

**docker-compose.yml**:
```yaml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=http://backend:8000
    depends_on:
      - backend

  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://user:pass@postgres:5432/scansmart
      - REDIS_URL=redis://redis:6379
      - MONGODB_URI=mongodb://mongo:27017/scansmart
    depends_on:
      - postgres
      - redis
      - mongo
    volumes:
      - ./storage:/app/storage

  celery_worker:
    build: ./backend
    command: celery -A app.worker worker --loglevel=info
    environment:
      - DATABASE_URL=postgresql://user:pass@postgres:5432/scansmart
      - REDIS_URL=redis://redis:6379
    depends_on:
      - postgres
      - redis

  celery_beat:
    build: ./backend
    command: celery -A app.worker beat --loglevel=info
    environment:
      - DATABASE_URL=postgresql://user:pass@postgres:5432/scansmart
      - REDIS_URL=redis://redis:6379
    depends_on:
      - postgres
      - redis

  postgres:
    image: timescale/timescaledb:latest-pg14
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=scansmart
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  mongo:
    image: mongo:6
    volumes:
      - mongo_data:/data/db
    ports:
      - "27017:27017"

  redis:
    image: redis:7-alpine
    volumes:
      - redis_data:/data
    ports:
      - "6379:6379"

volumes:
  postgres_data:
  mongo_data:
  redis_data:
```

**System Requirements**:
- CPU: 4+ cores (8+ recommended)
- RAM: 8GB minimum (16GB recommended)
- Storage: 50GB+ SSD
- Network: Stable broadband connection

#### Cloud Deployment (Optional)

**AWS Architecture**:
```
Route 53 (DNS)
    ↓
CloudFront (CDN)
    ↓
ALB (Load Balancer)
    ↓
ECS Fargate (Containers)
    ├── Frontend
    ├── Backend API
    └── Celery Workers
    ↓
RDS PostgreSQL + ElastiCache Redis + DocumentDB
```

**Cost Optimization for Single User**:
- Use smallest instance types
- Reserved instances for predictable workloads
- Spot instances for batch jobs
- S3 Intelligent-Tiering for storage

### 9. Security Architecture

#### Authentication & Authorization
**Method**: JWT (JSON Web Tokens)
**Flow**:
1. User login → Backend validates credentials
2. Backend issues JWT (access + refresh tokens)
3. Frontend stores JWT (httpOnly cookie or secure storage)
4. Each request includes JWT in Authorization header
5. Backend validates JWT on each request

**Implementation**:
```python
from fastapi import Depends, HTTPException
from fastapi.security import HTTPBearer
from jose import JWTError, jwt

security = HTTPBearer()

async def get_current_user(token: str = Depends(security)):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        user_id = payload.get("sub")
        if user_id is None:
            raise HTTPException(status_code=401)
        return user_id
    except JWTError:
        raise HTTPException(status_code=401)
```

#### Data Encryption
- **At Rest**: Database encryption (TDE)
- **In Transit**: TLS 1.3 for all connections
- **Sensitive Data**: Field-level encryption (API keys, passwords)

#### API Security
- Rate limiting per user/IP
- Input validation (Pydantic)
- SQL injection prevention (ORMs)
- XSS prevention (Content Security Policy)
- CSRF protection (same-site cookies)

### 10. Monitoring & Observability

#### Logging
**Stack**: Structured logging with ELK (Elasticsearch, Logstash, Kibana)
**Levels**:
- ERROR: System errors, exceptions
- WARN: Degraded performance, rate limits
- INFO: Business events (user actions, trades)
- DEBUG: Detailed debugging information

**Log Format**:
```json
{
  "timestamp": "2026-01-03T20:00:00Z",
  "level": "INFO",
  "service": "backend",
  "component": "catalyst_detector",
  "message": "New catalyst detected",
  "context": {
    "ticker": "AAPL",
    "catalyst_type": "earnings",
    "impact_score": 85
  }
}
```

#### Metrics
**Stack**: Prometheus + Grafana
**Key Metrics**:
- Request rate, latency, errors (RED method)
- Database query performance
- Cache hit rates
- ML model inference time
- Data ingestion lag
- Alert trigger frequency

**Dashboards**:
1. System Health: Overall status, errors, latency
2. Business Metrics: Active users, screens run, alerts sent
3. Data Pipeline: Ingestion rates, processing lag
4. ML Performance: Model accuracy, inference time

#### Alerting
**Tool**: Prometheus Alertmanager
**Alerts**:
- System down/degraded
- High error rates
- Database performance issues
- API quota approaching limits
- Disk space low

### 11. Performance Optimization

#### Caching Strategy
**Levels**:
1. **Browser Cache**: Static assets (CDN)
2. **Application Cache**: Redis (hot data)
3. **Database Cache**: Query results (materialized views)
4. **API Response Cache**: Frequent queries

**Cache Invalidation**:
- Time-based (TTL)
- Event-based (on data updates)
- Manual (admin override)

#### Query Optimization
- Database indexing strategy
- Query result pagination
- Lazy loading for large datasets
- N+1 query prevention (eager loading)

#### Async Processing
- Non-blocking I/O throughout
- Parallel API calls where possible
- Background job processing (Celery)
- WebSocket for real-time updates

### 12. Scalability Considerations

While optimized for single-user, the architecture can scale:

**Horizontal Scaling**:
- Stateless API servers (add more instances)
- Celery workers (add more workers)
- Database read replicas (read scaling)

**Vertical Scaling**:
- Increase server resources
- Database optimization
- Redis cluster mode

**Data Partitioning**:
- Partition by date (time-series data)
- Partition by ticker (market data)
- Shard by user (if multi-tenant)

### 13. Disaster Recovery

#### Backup Strategy
- **Database**: Daily automated backups, 30-day retention
- **Files**: Continuous backup to S3 or equivalent
- **Code**: Git repository (off-site)

#### Recovery Plan
- **RPO** (Recovery Point Objective): 24 hours
- **RTO** (Recovery Time Objective): 4 hours
- **Failover**: Automated database failover

### 14. Development Workflow

#### Local Development Setup
```bash
# Clone repository
git clone https://github.com/appleiolcanada-dot/Scansmart.git
cd Scansmart

# Start services with Docker Compose
docker-compose -f docker-compose.dev.yml up -d

# Install dependencies
cd frontend && npm install
cd ../backend && pip install -r requirements.txt

# Run database migrations
alembic upgrade head

# Start development servers
# Frontend: npm run dev (port 3000)
# Backend: uvicorn app.main:app --reload (port 8000)
```

#### CI/CD Pipeline
```yaml
# .github/workflows/ci.yml
name: CI/CD

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run tests
        run: |
          docker-compose -f docker-compose.test.yml up --abort-on-container-exit
      - name: Run linters
        run: |
          cd backend && pylint app/
          cd frontend && npm run lint
  
  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to production
        run: ./deploy.sh
```

## Conclusion

This architecture provides:
- **Modularity**: Easy to develop and test components independently
- **Performance**: Optimized for low latency and high throughput
- **Intelligence**: AI/ML integrated throughout
- **Scalability**: Can grow from single-user to multi-user
- **Reliability**: Robust error handling and monitoring
- **Security**: Multiple layers of protection
- **Maintainability**: Clean code structure and documentation

The system is designed to be the foundation for the world's most intelligent stock screener, with room to grow and adapt as requirements evolve.
