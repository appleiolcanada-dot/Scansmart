# Getting Started with Scansmart

This guide will help you get up and running with Scansmart quickly.

## Table of Contents
1. [System Requirements](#system-requirements)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [First Run](#first-run)
5. [Basic Usage](#basic-usage)
6. [Troubleshooting](#troubleshooting)

## System Requirements

### Minimum Requirements
- **CPU**: 2 cores
- **RAM**: 4GB
- **Storage**: 20GB SSD
- **OS**: Linux, macOS, or Windows 10+
- **Network**: Broadband internet connection

### Recommended Requirements
- **CPU**: 4+ cores (8+ preferred)
- **RAM**: 8GB (16GB preferred)
- **Storage**: 50GB+ SSD
- **OS**: Linux (Ubuntu 20.04+) or macOS
- **Network**: High-speed broadband

### Software Dependencies
- Docker 20.10+ and Docker Compose 2.0+
- (Optional) Node.js 18+ for frontend development
- (Optional) Python 3.10+ for backend development

## Installation

### Option 1: Docker (Recommended for Users)

This is the easiest way to get started. Everything runs in containers.

**Step 1: Install Docker**

**Linux (Ubuntu/Debian)**:
```bash
# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Add your user to docker group
sudo usermod -aG docker $USER
newgrp docker
```

**macOS**:
```bash
# Install Docker Desktop from https://www.docker.com/products/docker-desktop
# Or use Homebrew
brew install --cask docker
```

**Windows**:
Download and install Docker Desktop from https://www.docker.com/products/docker-desktop

**Step 2: Clone the Repository**
```bash
git clone https://github.com/appleiolcanada-dot/Scansmart.git
cd Scansmart
```

**Step 3: Set Up Environment Variables**
```bash
# Copy the example environment file
cp .env.example .env

# Edit the .env file with your settings
nano .env  # or use your favorite text editor
```

**Step 4: Start the Application**
```bash
# Start all services
docker-compose up -d

# Check if everything is running
docker-compose ps

# View logs
docker-compose logs -f
```

**Step 5: Access the Application**
- **Frontend**: http://localhost:3000
- **API**: http://localhost:8000
- **API Documentation**: http://localhost:8000/docs
- **Database** (PostgreSQL): localhost:5432
- **Cache** (Redis): localhost:6379

### Option 2: Local Development (For Developers)

This option gives you more control and is better for development.

**Step 1: Install Dependencies**

**Backend (Python)**:
```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
source venv/bin/activate  # Linux/macOS
# OR
venv\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt
```

**Frontend (Node.js)**:
```bash
cd frontend

# Install dependencies
npm install
# or
yarn install
```

**Step 2: Set Up Databases**

You can either:
- Run databases in Docker: `docker-compose up -d postgres mongo redis`
- Install locally (see database-specific documentation)

**Step 3: Configure Environment**

Create `.env` files in both `backend/` and `frontend/` directories.

**backend/.env**:
```env
DATABASE_URL=postgresql://scansmart:password@localhost:5432/scansmart
MONGODB_URI=mongodb://localhost:27017/scansmart
REDIS_URL=redis://localhost:6379

ALPHA_VANTAGE_API_KEY=your_key
POLYGON_API_KEY=your_key
NEWSAPI_KEY=your_key

JWT_SECRET=your-secret-key-change-this
ENCRYPTION_KEY=your-encryption-key-change-this
```

**frontend/.env.local**:
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_WS_URL=ws://localhost:8000
```

**Step 4: Initialize Database**

```bash
cd backend

# Run migrations
alembic upgrade head

# (Optional) Seed with sample data
python scripts/seed_data.py
```

**Step 5: Start Development Servers**

**Backend** (in one terminal):
```bash
cd backend
source venv/bin/activate
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

**Frontend** (in another terminal):
```bash
cd frontend
npm run dev
```

**Celery Worker** (in another terminal, for background jobs):
```bash
cd backend
source venv/bin/activate
celery -A app.worker worker --loglevel=info
```

**Celery Beat** (in another terminal, for scheduled jobs):
```bash
cd backend
source venv/bin/activate
celery -A app.worker beat --loglevel=info
```

## Configuration

### Getting API Keys

Scansmart requires API keys from various data providers. Here's how to get them:

#### 1. Alpha Vantage (Market Data)
- Visit: https://www.alphavantage.co/support/#api-key
- Free tier: 5 API calls per minute, 500 per day
- Sign up and copy your API key

#### 2. Polygon.io (Market Data - Alternative)
- Visit: https://polygon.io/
- Free tier: 5 API calls per minute
- Better for real-time data (paid tiers)
- Sign up and copy your API key

#### 3. NewsAPI (News Data)
- Visit: https://newsapi.org/register
- Free tier: 100 requests per day (limited to 1 month history)
- Developer plan: $449/month (for production)
- Copy your API key

#### 4. Finnhub (News & Sentiment)
- Visit: https://finnhub.io/register
- Free tier: 60 API calls per minute
- Sign up and copy your API key

#### 5. Twitter API (Social Sentiment - Optional)
- Visit: https://developer.twitter.com/
- Apply for developer account
- Create an app and get Bearer Token
- Free tier has rate limits

#### 6. Reddit API (Social Sentiment - Optional)
- Visit: https://www.reddit.com/prefs/apps
- Create an app (script type)
- Get client ID and secret

### Environment Variables Reference

**Required**:
```env
# Database connections
DATABASE_URL=postgresql://user:pass@host:5432/dbname
REDIS_URL=redis://host:6379

# Security
JWT_SECRET=change-this-to-a-random-string
ENCRYPTION_KEY=32-byte-random-key

# At least one market data source
ALPHA_VANTAGE_API_KEY=your_key
# OR
POLYGON_API_KEY=your_key
```

**Optional**:
```env
# Additional data sources
NEWSAPI_KEY=your_key
FINNHUB_API_KEY=your_key
TWITTER_BEARER_TOKEN=your_token
REDDIT_CLIENT_ID=your_id
REDDIT_CLIENT_SECRET=your_secret

# MongoDB (for document storage)
MONGODB_URI=mongodb://host:27017/dbname

# Email notifications
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# SMS notifications (Twilio)
TWILIO_ACCOUNT_SID=your_sid
TWILIO_AUTH_TOKEN=your_token
TWILIO_PHONE_NUMBER=+1234567890

# Monitoring (optional)
SENTRY_DSN=your_sentry_dsn
```

### Generating Secrets

**JWT Secret**:
```bash
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

**Encryption Key**:
```bash
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
```

## First Run

### 1. Create Your Account

Navigate to http://localhost:3000 and click "Sign Up"

Fill in:
- Email
- Password (min 8 characters)
- Name (optional)

### 2. Set Your Preferences

After logging in, go to Settings → Preferences:
- **Trading Style**: Day trader, swing trader, position trader, or investor
- **Risk Tolerance**: Conservative, moderate, or aggressive
- **Preferred Sectors**: Select sectors you're interested in
- **Market Cap**: Large, mid, small, or micro cap
- **Exclusions**: Sectors or stock types to exclude

### 3. Explore the Dashboard

The dashboard shows:
- **Top Opportunities**: AI-selected stocks based on your preferences
- **Active Catalysts**: Recent catalyst events
- **Your Portfolio**: If you add positions
- **Custom Screens**: Your saved screening criteria

### 4. Create Your First Screen

**Example: Finding Earnings Plays**

1. Click "Screening" in the navigation
2. Click "New Screen"
3. Add filters:
   - Catalyst Type: Earnings
   - Catalyst Timing: Next 14 days
   - Historical Beat Rate: > 60%
   - RSI: 30-70 (not overbought/oversold)
   - Market Cap: > $1B
4. Set score weights (or use defaults)
5. Click "Run Screen"
6. Save the screen for later use

### 5. Set Up Alerts

**Example: Biotech FDA Alerts**

1. Click "Alerts" in the navigation
2. Click "New Alert"
3. Configure:
   - Type: Catalyst Alert
   - Catalyst Type: FDA
   - Sector: Healthcare
   - Min Impact Score: 80
   - Delivery: Email + In-app
4. Save alert

Now you'll be notified when high-impact FDA catalysts are detected!

### 6. Add Stocks to Watchlist

1. Search for a stock or find one in screening results
2. Click the "Add to Watchlist" button
3. Create a new watchlist or add to existing
4. Set alerts for watchlist stocks (optional)

## Basic Usage

### Running a Quick Screen

**Via Web UI**:
1. Navigate to Screening page
2. Use preset screens (FDA Catalysts, Earnings Momentum, etc.)
3. Or create custom screen with filters
4. Results show ranked by intelligence score

**Via CLI** (if installed):
```bash
# Install CLI
pip install scansmart-cli

# Login
scansmart login --email your@email.com

# Run a quick screen
scansmart screen --catalyst-type earnings --days 14 --min-score 80

# Save results to CSV
scansmart screen --catalyst-type earnings --days 14 --output results.csv
```

**Via API**:
```bash
# Get auth token
TOKEN=$(curl -X POST http://localhost:8000/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"your@email.com","password":"yourpass"}' \
  | jq -r '.access_token')

# Run screen
curl -X POST http://localhost:8000/api/v1/screen \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "filters": {
      "catalyst_type": "earnings",
      "catalyst_timing": {"max_days": 14},
      "market_cap": {"min": 1000000000}
    },
    "limit": 20
  }' | jq
```

### Viewing Catalyst Feed

**Web UI**:
1. Click "Catalysts" in navigation
2. See real-time feed of detected catalysts
3. Filter by type, sector, or impact
4. Click on catalyst for details

**API**:
```bash
# Get active catalysts
curl http://localhost:8000/api/v1/catalysts/active?limit=20 \
  -H "Authorization: Bearer $TOKEN" | jq

# Get catalyst calendar
curl http://localhost:8000/api/v1/catalysts/calendar?days=30 \
  -H "Authorization: Bearer $TOKEN" | jq
```

### Adding to Portfolio

**Web UI**:
1. Click "Portfolio" in navigation
2. Click "Add Position"
3. Enter:
   - Ticker
   - Shares
   - Entry price
   - Entry date
4. Save

**API**:
```bash
curl -X POST http://localhost:8000/api/v1/portfolio/positions \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "ticker": "AAPL",
    "shares": 100,
    "entry_price": 150.00,
    "entry_date": "2026-01-01"
  }'
```

### Running a Backtest

**Web UI**:
1. Go to Screening page
2. Create or select a screen
3. Click "Backtest" button
4. Select date range
5. Configure entry/exit rules
6. Run backtest
7. View results and equity curve

**API**:
```bash
curl -X POST http://localhost:8000/api/v1/backtest \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "screen_id": "your-screen-id",
    "start_date": "2023-01-01",
    "end_date": "2025-12-31",
    "initial_capital": 10000,
    "position_size": 0.1,
    "hold_days": 10
  }' | jq
```

## Troubleshooting

### Common Issues

#### 1. Docker containers won't start

**Problem**: `docker-compose up` fails
```
Error: Cannot start service postgres: driver failed programming external connectivity
```

**Solution**:
- Check if ports are already in use: `netstat -an | grep LISTEN`
- Change ports in `docker-compose.yml` if needed
- Or stop conflicting services

#### 2. API returns "Invalid API key"

**Problem**: Market data endpoints return 401 or 403 errors

**Solution**:
- Verify API key in `.env` file
- Check API key is active on provider's dashboard
- Ensure you haven't exceeded rate limits
- Check API key format (no extra spaces)

#### 3. Database connection errors

**Problem**: `sqlalchemy.exc.OperationalError: could not connect to server`

**Solution**:
- Ensure PostgreSQL is running: `docker-compose ps postgres`
- Check DATABASE_URL format: `postgresql://user:pass@host:port/dbname`
- Verify credentials match docker-compose.yml
- Try: `docker-compose restart postgres`

#### 4. Frontend can't connect to API

**Problem**: Network error or CORS error in browser console

**Solution**:
- Verify backend is running: `curl http://localhost:8000/health`
- Check NEXT_PUBLIC_API_URL in frontend/.env.local
- Ensure CORS is configured in backend (should be by default)
- Try clearing browser cache

#### 5. Slow performance

**Problem**: Queries taking too long, UI laggy

**Solution**:
- Check database indexes: `python scripts/check_indexes.py`
- Increase Redis memory: Edit docker-compose.yml
- Optimize queries with `EXPLAIN ANALYZE`
- Consider increasing hardware resources
- Check API rate limiting (hitting limits?)

#### 6. Missing data

**Problem**: Stocks not appearing in screens, no catalyst data

**Solution**:
- Check if initial data load completed: `docker-compose logs celery_worker`
- Manually trigger data refresh: `python scripts/refresh_data.py`
- Verify API keys are working: `python scripts/test_apis.py`
- Check celery beat is running: `docker-compose ps celery_beat`

#### 7. Email notifications not working

**Problem**: Alerts not being delivered via email

**Solution**:
- Verify SMTP settings in `.env`
- For Gmail, use App Password (not regular password)
- Check spam/junk folder
- Test SMTP connection: `python scripts/test_email.py`
- Check email logs: `docker-compose logs backend | grep email`

### Getting Help

If you're still having issues:

1. **Check Logs**:
   ```bash
   # All services
   docker-compose logs
   
   # Specific service
   docker-compose logs backend
   docker-compose logs frontend
   
   # Follow logs in real-time
   docker-compose logs -f
   ```

2. **Check System Status**:
   ```bash
   # Container status
   docker-compose ps
   
   # Resource usage
   docker stats
   
   # Disk space
   df -h
   ```

3. **Search Issues**: Check [GitHub Issues](https://github.com/appleiolcanada-dot/Scansmart/issues)

4. **Ask for Help**: Create a new issue with:
   - Description of problem
   - Steps to reproduce
   - Log output
   - System information (OS, Docker version)

## Next Steps

Now that you're set up, explore:

1. **[FEATURES.md](./FEATURES.md)**: Learn about all features in detail
2. **[ARCHITECTURE.md](./ARCHITECTURE.md)**: Understand how everything works
3. **[API Documentation](http://localhost:8000/docs)**: Explore the API
4. **User Guide** (coming soon): Step-by-step tutorials
5. **Video Tutorials** (coming soon): Visual walkthroughs

Happy screening! 🚀
