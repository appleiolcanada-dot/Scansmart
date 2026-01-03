# Frequently Asked Questions (FAQ)

## Table of Contents
- [General Questions](#general-questions)
- [Getting Started](#getting-started)
- [Features & Functionality](#features--functionality)
- [Pricing & Plans](#pricing--plans)
- [Technical Questions](#technical-questions)
- [Data & Privacy](#data--privacy)
- [Troubleshooting](#troubleshooting)
- [Strategy & Trading](#strategy--trading)

---

## General Questions

### What is Scansmart?

Scansmart is an AI-powered stock screener that focuses on **catalysts**—the events that actually move stocks. Unlike traditional screeners that only show historical metrics, Scansmart uses artificial intelligence to detect upcoming catalysts, predict their impact, and personalize recommendations to your trading style.

### How is Scansmart different from other stock screeners?

**Key differences:**
1. **Catalyst-First**: Focuses on events that drive future movement, not just historical data
2. **AI-Powered**: Uses machine learning for prediction and personalization
3. **Composite Intelligence**: Combines technical, fundamental, catalyst, and sentiment analysis
4. **Single-User Optimized**: Designed for individual traders, not institutions
5. **Proactive**: Alerts you to opportunities before they move

See our [Competitive Analysis](./COMPETITIVE_ANALYSIS.md) for detailed comparisons.

### Who is Scansmart for?

**Ideal users:**
- Active day and swing traders
- Catalyst-focused investors
- Earnings players
- Biotech/pharma traders
- Anyone wanting intelligent, actionable stock insights

**Not ideal for:**
- Completely passive investors (buy and hold forever)
- Those wanting only free tools
- Institutional traders (Bloomberg is better for institutions)

### Do I need trading experience to use Scansmart?

**Basic knowledge helpful, but not required.**

- **Beginners**: Start with preset screens and educational resources
- **Intermediate**: Create custom screens and use backtesting
- **Advanced**: Leverage API, advanced analytics, and personalization

We provide a comprehensive [Glossary](./GLOSSARY.md) and tutorials to help you learn.

### What markets does Scansmart cover?

**Current focus:**
- US stock markets (NYSE, NASDAQ, AMEX)
- 5,000+ publicly traded companies

**Future plans:**
- International markets (UK, Europe, Asia)
- ETFs and mutual funds
- Cryptocurrencies
- Forex and commodities

---

## Getting Started

### How do I sign up?

1. Visit https://scansmart.io (when launched)
2. Click "Sign Up"
3. Enter email and create password
4. Verify email
5. Complete onboarding (preferences)
6. Start screening!

### What do I need to get started?

**Minimum:**
- Email address
- Internet connection
- Modern web browser (Chrome, Firefox, Safari, Edge)

**Recommended:**
- API keys from data providers (see [Data Sources](./DATA_SOURCES.md))
- Basic understanding of stock trading
- Clear trading goals and style

### Is there a free trial?

Yes! Free trial details:
- 14 days full access
- No credit card required
- All features unlocked
- No obligations

After trial, choose a paid plan or downgrade to free tier (limited features).

### Can I use Scansmart on mobile?

**Yes!** Scansmart is a Progressive Web App (PWA):
- Works on any device with a browser
- Install as app on iOS/Android
- Offline capabilities
- Push notifications
- Optimized mobile interface

### Do I need to download software?

**No.** Scansmart is entirely web-based. Just open your browser and go.

For advanced users, we offer:
- CLI tools (command line interface)
- API access (programmatic access)
- Both optional, not required

---

## Features & Functionality

### What is a "catalyst"?

A catalyst is an event that causes significant stock price movement. Examples:
- Earnings reports
- FDA drug approvals
- Merger announcements
- Product launches
- CEO changes
- Legal outcomes

Scansmart detects, tracks, and predicts the impact of these catalysts automatically.

### How accurate are the catalyst predictions?

**Impact predictions:**
- Trained on thousands of historical events
- Typically 70-80% accuracy in direction
- Magnitude predictions have wider confidence intervals
- Improves over time with more data

**Important**: No prediction is 100% accurate. Always do your own due diligence and manage risk appropriately.

### What is the Intelligence Score?

The Intelligence Score (0-100) is Scansmart's proprietary composite ranking:
- **Catalyst Score (40%)**: Event impact and timing
- **Technical Score (25%)**: Chart setup and momentum
- **Fundamental Score (20%)**: Financial health and valuation
- **Sentiment Score (10%)**: News and social buzz
- **Timing Score (5%)**: Optimal entry window

Higher scores indicate better opportunities based on your preferences.

### Can I create custom screens?

**Yes!** Multiple ways to screen:
1. **Preset Screens**: Use our expert-designed screens
2. **Custom Screens**: Build your own with drag-and-drop filters
3. **Natural Language**: Type in plain English what you want
4. **Clone & Modify**: Start with a preset and customize

Save unlimited screens on paid plans.

### How do alerts work?

**Alert types:**
- Catalyst alerts (new events detected)
- Price alerts (level breaches)
- Screening alerts (new matches)
- Portfolio alerts (holdings affected)
- Personalized alerts (AI suggestions)

**Delivery options:**
- In-app notifications
- Email
- SMS (Pro/Elite plans)
- Push notifications (mobile)
- Webhook (API access)

### Can I backtest strategies?

**Yes!** Backtesting features:
- Test any screen on historical data
- Configure entry/exit rules
- See performance metrics (return, Sharpe, drawdown)
- Compare to benchmarks
- Visualize equity curve
- Export results

Available on Pro and Elite plans.

### Does Scansmart execute trades?

**No.** Scansmart is a research and analysis tool, not a broker.

We provide:
- Intelligence and insights
- Opportunities and alerts
- Analysis and research

You execute trades with your broker. In the future, we may add read-only brokerage integration for portfolio tracking.

---

## Pricing & Plans

### How much does Scansmart cost?

**Pricing tiers** (planned):

**Free Tier**
- Basic screening (3 filters max)
- 5 screens saved
- Price alerts only
- Limited catalyst detection
- Ads supported

**Pro Tier** ($49/month or $470/year)
- Advanced screening (unlimited filters)
- Unlimited saved screens
- All alert types
- Full catalyst detection
- AI sentiment analysis
- Backtesting
- Email support

**Elite Tier** ($149/month or $1,490/year)
- Everything in Pro
- Real-time data
- Advanced ML predictions
- API access (10,000 calls/month)
- SMS alerts
- Priority support
- Custom ML models

### Is there an annual discount?

**Yes!** Save 20% with annual billing:
- Pro: $470/year (vs $588/year monthly)
- Elite: $1,490/year (vs $1,788/year monthly)

### Can I cancel anytime?

**Yes.** No long-term commitments:
- Cancel anytime from settings
- Access continues through paid period
- No cancellation fees
- Can reactivate later

### Do you offer refunds?

**14-day money-back guarantee:**
- Full refund within 14 days
- No questions asked
- Email support@scansmart.io

### Are there discounts for students or educators?

**Student Discount**: 50% off Pro plan
- Must verify student status
- Annual renewal required

**Educator Program**: Free Elite access
- Must be teaching finance/trading
- Require institutional email

### Can I bring my own API keys?

**Yes!** (Elite plan feature)
- Use your own data API keys
- Reduces our costs = we pass savings to you
- More control over data sources
- Can upgrade to better data plans

---

## Technical Questions

### What browsers are supported?

**Fully supported:**
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

**Mobile browsers:**
- iOS Safari 14+
- Chrome Mobile
- Firefox Mobile

**Not supported:**
- Internet Explorer (discontinued)
- Opera Mini
- Browsers with JavaScript disabled

### Can I self-host Scansmart?

**Not officially**, but Scansmart is open source (MIT license):
- You CAN self-host for personal use
- Code available on GitHub
- Docker Compose for easy setup
- See [Getting Started](./GETTING_STARTED.md)

**No support provided for self-hosted instances.**

### What are the system requirements for self-hosting?

**Minimum:**
- 2 CPU cores
- 4GB RAM
- 20GB storage
- Docker installed

**Recommended:**
- 4+ CPU cores
- 8GB+ RAM
- 50GB+ SSD
- Linux/macOS host

See [Architecture](./ARCHITECTURE.md) for details.

### Is there an API?

**Yes!** (Elite plan)
- RESTful API
- WebSocket for real-time
- Comprehensive documentation
- Rate limited by plan
- API keys for authentication

**Use cases:**
- Custom integrations
- Automated strategies
- External dashboards
- Zapier/IFTTT automation

### Can I integrate with my broker?

**Planned but not yet available:**
- Read-only integration for portfolio sync
- No automatic trading (intentional)
- Support for major brokers (TD, Schwab, IBKR, etc.)

Currently, manually add positions for portfolio tracking.

---

## Data & Privacy

### Where does the data come from?

**Multiple sources:**
- Market data: Alpha Vantage, Polygon.io, Yahoo Finance
- News: NewsAPI, Finnhub
- Social: Reddit, Twitter (optional)
- Government: SEC EDGAR, FDA OpenData
- Economic: FRED (Federal Reserve)

See [Data Sources](./DATA_SOURCES.md) for complete list.

### How fresh is the data?

**Depends on plan:**
- Free: 15-minute delayed quotes
- Pro: 1-minute delayed quotes
- Elite: Real-time quotes

**Other data:**
- Catalysts: Real-time detection
- News: 1-5 minute delay
- Fundamentals: Daily updates
- SEC filings: Real-time

### Is my data private?

**Yes. We take privacy seriously:**
- Your screens and alerts are private
- Portfolio data is encrypted
- No selling of user data
- GDPR & CCPA compliant
- Can export or delete your data anytime

### What data do you collect?

**Personal data:**
- Email (required)
- Name (optional)
- Payment info (via Stripe, we don't store)

**Usage data:**
- Feature usage (anonymized analytics)
- Screen and alert configurations
- Error logs (no sensitive data)

**Trading data:**
- Portfolio positions (if you add them)
- Watchlists
- Preferences

See [Privacy Policy](./PRIVACY.md) for complete details.

### Do you use my data to train AI models?

**Anonymized and aggregated data only:**
- We use aggregate patterns to improve models
- Individual user data is not used directly
- You can opt out of analytics in settings
- Screened/anomalyzed data only, never personal data

### Can I delete my account and data?

**Yes, anytime:**
1. Go to Settings → Account
2. Click "Delete Account"
3. Confirm deletion
4. All data permanently deleted within 30 days

Or email support@scansmart.io for manual deletion.

---

## Troubleshooting

### Why are my screens not showing results?

**Common issues:**
1. **Too many filters**: Relax some criteria
2. **Data not loaded**: Wait for initial data sync (check status)
3. **Market closed**: Some filters need live data
4. **API limits reached**: Check API usage in settings

**Solution**: Start with fewer filters and add gradually.

### Why am I not getting alerts?

**Check:**
1. **Alerts enabled**: Settings → Notifications
2. **Email verified**: Check spam folder
3. **Alert criteria too narrow**: Broaden parameters
4. **Quiet hours active**: Check notification schedule
5. **Browser notifications**: Allow in browser settings

### The app is slow or freezing

**Try:**
1. **Clear cache**: Settings → Clear Cache
2. **Close other tabs**: Free up browser memory
3. **Update browser**: Use latest version
4. **Disable extensions**: Try in private/incognito mode
5. **Check internet**: Run speed test

Still slow? Report to support with browser/device info.

### I'm seeing incorrect stock data

**Possible causes:**
1. **Data delay**: Check your plan's delay time
2. **Source issue**: Data provider may have error
3. **Cache**: Try refreshing data
4. **Split/dividend**: Recent corporate action not adjusted

**Report it**: Help us improve data quality by reporting errors.

### How do I report a bug?

**Options:**
1. **In-app**: Click feedback button
2. **GitHub**: Open issue at https://github.com/appleiolcanada-dot/Scansmart/issues
3. **Email**: support@scansmart.io

**Include:**
- Description of issue
- Steps to reproduce
- Screenshots (if applicable)
- Browser and device info

---

## Strategy & Trading

### Should I trade every high-scoring stock?

**No!** The Intelligence Score is a starting point, not a guarantee:
- Do your own research
- Consider your risk tolerance
- Size positions appropriately
- Have a plan (entry, exit, stop loss)
- Diversify (don't bet everything on one stock)

**Scansmart provides intelligence, not investment advice.**

### How should I use catalyst information?

**Best practices:**
1. **Research the catalyst**: Understand what it means
2. **Check historical outcomes**: How did similar catalysts perform?
3. **Consider timing**: Are you early or late?
4. **Assess risk**: What if it goes the other way?
5. **Have an exit plan**: When will you take profit or cut losses?

### Can Scansmart guarantee profits?

**No.** Nothing can guarantee profits in trading:
- All trading involves risk
- Past performance doesn't guarantee future results
- AI predictions are probabilistic, not certain
- Always be prepared to lose your investment

**Use Scansmart as one tool in your arsenal, not your only tool.**

### What's the best screening strategy?

**It depends on your:**
- Trading style (day, swing, position)
- Risk tolerance
- Time commitment
- Market knowledge
- Goals

**Start with:**
1. Try preset screens to learn
2. Identify what you like
3. Customize to your style
4. Backtest your strategy
5. Start small, scale gradually

### Should I use all the filters?

**No, less is often more:**
- Start with 3-5 key criteria
- Too many filters = fewer results
- Focus on what matters most
- Let the AI score handle complexity

**Quality over quantity.**

### How often should I check Scansmart?

**Depends on your style:**
- **Day traders**: Multiple times during market hours
- **Swing traders**: Daily before/after market
- **Position traders**: 2-3 times per week
- **Long-term investors**: Weekly

**Pro tip**: Set up alerts so Scansmart notifies you, rather than constantly checking.

---

## Still Have Questions?

### Resources
- [Documentation](./README.md)
- [Getting Started Guide](./GETTING_STARTED.md)
- [Glossary](./GLOSSARY.md)
- [Video Tutorials](#) (coming soon)

### Support Channels
- **Email**: support@scansmart.io
- **GitHub Issues**: https://github.com/appleiolcanada-dot/Scansmart/issues
- **Community Forum**: https://community.scansmart.io (coming soon)
- **Twitter**: [@scansmart](https://twitter.com/scansmart) (coming soon)

### Response Times
- **Free users**: 48-72 hours (email only)
- **Pro users**: 24 hours (email)
- **Elite users**: 4 hours (priority email)
- **Critical issues**: Best effort for all users

---

**Last Updated**: January 2026

**Note**: This FAQ will be updated regularly as Scansmart evolves and based on common user questions.
