# Scansmart 🚀

**The World's Most Intelligent Stock Screener for Single Person Use**

AI-Powered Catalyst-First Stock Screener

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: Planning](https://img.shields.io/badge/Status-Planning-blue.svg)]()

---

## 🎯 What Makes Scansmart Different?

Scansmart isn't just another stock screener. It's an **AI-powered intelligence platform** that focuses on **catalysts**—the events that actually move stocks—not just historical metrics.

### The Problem with Traditional Screeners
- **Backward-looking**: Focus on what happened, not what will happen
- **Information overload**: Too much data, not enough insight
- **One-size-fits-all**: Built for institutions, not individuals
- **Reactive**: You find opportunities after they've moved

### The Scansmart Solution
- **Catalyst-first**: Focus on events that drive future movement
- **AI-powered**: Intelligent filtering and prediction, not just data display
- **Personalized**: Learns your style and preferences
- **Proactive**: Alerts you to opportunities before others see them

---

## ✨ Key Features

### 🧠 Intelligent Catalyst Detection
- **Real-time monitoring** of news, SEC filings, earnings, FDA approvals, and more
- **AI classification** of catalyst types and impact
- **Predictive analytics** for expected price movement
- **Historical outcome tracking** to learn what works

### 📊 Multi-Dimensional Screening
- **Technical filters**: Price, volume, momentum, patterns
- **Fundamental filters**: Valuation, growth, quality, financials
- **Catalyst filters**: Type, timing, impact, success rate
- **Sentiment filters**: News, social media, analyst, insider activity

### 🎯 Composite Intelligence Score
Each stock receives a 0-100 score based on:
- **Catalyst Strength** (40%): Impact probability and timing
- **Technical Setup** (25%): Chart position and momentum
- **Fundamental Quality** (20%): Valuation and growth
- **Sentiment** (10%): News and social buzz
- **Timing** (5%): Optimal entry window

### 🔔 Smart Alert System
- **Catalyst alerts**: Immediate notification of breaking events
- **Price alerts**: Technical level breaches
- **Screening alerts**: New stocks matching your criteria
- **AI suggestions**: Personalized opportunities
- **Anti-noise filtering**: Only relevant, actionable alerts

### 📈 Portfolio & Research Hub
- **Portfolio tracking** with catalyst impact analysis
- **Risk analytics** and diversification insights
- **Comprehensive research** tools (news, filings, competitors)
- **Backtesting** to validate strategies
- **Opportunity cost** analysis

### 🤖 AI Personalization
- **Learns your preferences** from behavior
- **Adaptive scoring** based on your success patterns
- **Custom recommendations** tailored to you
- **Smart defaults** that improve over time

---

## 📚 Documentation

- **[ANALYSIS.md](./ANALYSIS.md)**: Comprehensive analysis of what makes this the world's most intelligent stock screener
- **[ARCHITECTURE.md](./ARCHITECTURE.md)**: Technical architecture and system design
- **[FEATURES.md](./FEATURES.md)**: Detailed feature specifications
- **[ROADMAP.md](./ROADMAP.md)**: 12-month implementation plan

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│                  Client Layer                            │
│        React/Next.js + Mobile PWA + CLI Tools            │
└─────────────────────────────────────────────────────────┘
                         │
┌─────────────────────────────────────────────────────────┐
│                  API Gateway                             │
│           FastAPI + WebSocket + JWT Auth                 │
└─────────────────────────────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
┌───────▼──────┐  ┌──────▼──────┐  ┌────▼─────┐
│  Screening   │  │   AI/ML     │  │   Data   │
│   Engine     │  │   Engine    │  │  Pipeline│
└──────────────┘  └─────────────┘  └──────────┘
                         │
┌─────────────────────────────────────────────────────────┐
│              Data Storage Layer                          │
│  PostgreSQL + TimescaleDB + MongoDB + Redis              │
└─────────────────────────────────────────────────────────┘
                         │
┌─────────────────────────────────────────────────────────┐
│            External Data Sources                         │
│  Market APIs + News + Social + SEC + FDA                 │
└─────────────────────────────────────────────────────────┘
```

### Technology Stack
- **Backend**: Python, FastAPI, Celery, Redis
- **Frontend**: React, Next.js, TailwindCSS, shadcn/ui
- **AI/ML**: PyTorch, Transformers, scikit-learn
- **Databases**: PostgreSQL (TimescaleDB), MongoDB, Redis
- **Infrastructure**: Docker, Docker Compose
- **APIs**: Alpha Vantage, Polygon, NewsAPI, SEC EDGAR, FDA

---

## 🚀 Getting Started

### Prerequisites
- Docker & Docker Compose
- Node.js 18+ (for local frontend development)
- Python 3.10+ (for local backend development)

### Quick Start with Docker (Recommended)

```bash
# Clone the repository
git clone https://github.com/appleiolcanada-dot/Scansmart.git
cd Scansmart

# Copy environment template
cp .env.example .env

# Add your API keys to .env
nano .env

# Start all services
docker-compose up -d

# Access the application
# Frontend: http://localhost:3000
# API: http://localhost:8000
# API Docs: http://localhost:8000/docs
```

### Local Development Setup

**Backend**:
```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
alembic upgrade head
uvicorn app.main:app --reload
```

**Frontend**:
```bash
cd frontend
npm install
npm run dev
```

### Configuration

Create a `.env` file with required API keys:

```env
# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/scansmart
MONGODB_URI=mongodb://localhost:27017/scansmart
REDIS_URL=redis://localhost:6379

# Market Data
ALPHA_VANTAGE_API_KEY=your_key_here
POLYGON_API_KEY=your_key_here

# News & Sentiment
NEWSAPI_KEY=your_key_here
FINNHUB_API_KEY=your_key_here

# Security
JWT_SECRET=your_secret_here
ENCRYPTION_KEY=your_encryption_key_here

# Email (Optional)
SMTP_HOST=smtp.gmail.com
SMTP_USER=your_email
SMTP_PASS=your_password
```

---

## 📖 Usage Examples

### Example 1: Find Biotech Catalysts

```python
# Using Python API client
from scansmart import ScansmartClient

client = ScansmartClient(api_key="your_key")

# Find biotech stocks with upcoming FDA catalysts
results = client.screen({
    "sector": "Healthcare",
    "industry": "Biotechnology",
    "catalyst_type": "FDA",
    "catalyst_timing": {"max_days": 30},
    "market_cap": {"min": 500000000},
    "score": {"min": 80}
})

for stock in results:
    print(f"{stock.ticker}: Score {stock.score}/100")
    print(f"  Catalyst: {stock.catalyst.description}")
    print(f"  Expected Impact: {stock.catalyst.predicted_impact}%")
```

### Example 2: Earnings Momentum Screen

```javascript
// Using JavaScript API client
import { ScansmartClient } from 'scansmart-js';

const client = new ScansmartClient({ apiKey: 'your_key' });

// Find stocks with strong earnings momentum
const results = await client.screen({
  catalyst_type: 'earnings',
  catalyst_timing: { max_days: 14 },
  earnings_surprise: { min: 5 },
  revenue_growth: { min: 15 },
  technical_score: { min: 70 }
});

results.forEach(stock => {
  console.log(`${stock.ticker}: ${stock.score}/100`);
});
```

### Example 3: Set Up Alerts

```bash
# Using CLI
scansmart alert create \
  --type catalyst \
  --ticker AAPL \
  --channels email,sms \
  --priority high

# Alert on new screens
scansmart alert create \
  --type screen \
  --screen-id "my-earnings-screen" \
  --min-score 85
```

---

## 🗺️ Roadmap

### ✅ Phase 1: MVP (Months 1-3)
- Basic stock screening
- Market data integration
- User authentication
- Simple alerts
- Portfolio tracking

### 🚧 Phase 2: Intelligence (Months 4-6) - Current
- AI catalyst detection
- Sentiment analysis
- Composite scoring
- Pattern recognition
- Enhanced alerts

### 📅 Phase 3: Advanced (Months 7-9)
- Catalyst impact prediction
- Backtesting framework
- Personalization engine
- Research hub
- Portfolio analytics

### 🔮 Phase 4: Scale (Months 10-12)
- Mobile PWA
- Performance optimization
- Advanced charting
- Public API
- Educational content

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](./CONTRIBUTING.md) for details.

### Development Process
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Standards
- Follow PEP 8 for Python
- Use ESLint config for JavaScript/TypeScript
- Write tests for new features
- Update documentation

---

## 📊 Project Status

**Current Phase**: Planning & Design
**Version**: 0.1.0-alpha
**Last Updated**: January 2026

### Recent Updates
- ✅ Complete analysis document
- ✅ Architecture design
- ✅ Feature specifications
- ✅ 12-month roadmap
- 🚧 MVP development starting

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

---

## 🙏 Acknowledgments

- Inspired by professional trading tools like Bloomberg Terminal
- Built with amazing open-source technologies
- Designed for individual traders and investors

---

## 📞 Contact & Support

- **Issues**: [GitHub Issues](https://github.com/appleiolcanada-dot/Scansmart/issues)
- **Discussions**: [GitHub Discussions](https://github.com/appleiolcanada-dot/Scansmart/discussions)
- **Email**: support@scansmart.io (coming soon)
- **Twitter**: [@scansmart](https://twitter.com/scansmart) (coming soon)

---

## 🌟 Star History

If you find Scansmart useful, please consider giving it a star! ⭐

---

**Made with ❤️ for individual traders and investors**
