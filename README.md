# Awesome AI Trading MCP

A curated, fact-checked map of **MCP servers** and **open-source AI tools** for trading, market data and "vibe trading" (describe a strategy in plain English → an AI agent codes, backtests and optionally runs it).

> **Snapshot date: 2026-11-02.** GitHub stars, licences and last-push dates were checked against the GitHub API on that date. Everything else (hosted endpoints, launch dates, features) comes from vendor docs and press coverage linked in each row — re-check before connecting a funded account.
>
> **Not financial advice.** Nothing here is a recommendation to trade. Start read-only or in paper mode.

## Contents

- [The one rule](#the-one-rule)
- [Quick picks](#quick-picks)
- [Vibe trading and AI trading agents](#vibe-trading-and-ai-trading-agents)
- [Quant platforms and financial foundation models](#quant-platforms-and-financial-foundation-models)
- [Free market-data MCPs](#free-market-data-mcps)
- [Official broker MCPs](#official-broker-mcps)
- [Official crypto exchange MCPs](#official-crypto-exchange-mcps)
- [Forex and CFD](#forex-and-cfd)
- [Keyed market-data MCPs](#keyed-market-data-mcps)
- [Crypto analytics, on-chain and sentiment MCPs](#crypto-analytics-on-chain-and-sentiment-mcps)
- [Institutional data (Claude for Financial Services)](#institutional-data-claude-for-financial-services)
- [Prediction markets](#prediction-markets)
- [Research, backtesting and charting MCPs](#research-backtesting-and-charting-mcps)
- [Trading engines, bots and backtesting libraries](#trading-engines-bots-and-backtesting-libraries)
- [Where the free data actually comes from](#where-the-free-data-actually-comes-from)
- [Safety checklist](#safety-checklist)
- [Related lists](#related-lists)
- [Methodology](#methodology)

## The one rule

- **Placing real orders always needs auth** (OAuth or an API key) — no exceptions.
- **Free with no auth** covers market data, indicators, screening, backtesting, research and simulated trading.
- Most "free, no key" stock servers read **Yahoo Finance through `yfinance`**, which is unofficial. Five Yahoo-based servers are still **one** source.

## Quick picks

| Need | Pick | Cost / auth |
|---|---|---|
| Vibe trading (plain English → backtest) | [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | Free; no data keys; local LLM via Ollama = no keys at all |
| Multi-agent research (bull vs bear debate) | [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | Free; supports Ollama and OpenAI-compatible local servers |
| Quant ML research platform | [microsoft/qlib](https://github.com/microsoft/qlib) | Free |
| Free stock-data MCP, local | [wshobson/maverick-mcp](https://github.com/wshobson/maverick-mcp) | Free, no key |
| Charts / screener MCP | [atilaahmettaner/tradingview-mcp](https://github.com/atilaahmettaner/tradingview-mcp) | Free self-hosted |
| Crypto data | [CoinGecko official MCP](https://docs.coingecko.com/docs/mcp-server) `mcp.api.coingecko.com/mcp` | Free keyless endpoint (beta) |
| Company filings | [stefanoamorelli/sec-edgar-mcp](https://github.com/stefanoamorelli/sec-edgar-mcp) | Free, no key (User-Agent only) |
| Macro data | [FRED MCP Connector](https://fred.stlouisfed.org/help/data/connecting-fred-to-ai-services/FRED-MCP-Connector) (official) | Free, needs a free connector account |
| Paper trading | [alpacahq/alpaca-mcp-server](https://github.com/alpacahq/alpaca-mcp-server) | Free account + key; paper by default |
| Crypto bot | [freqtrade/freqtrade](https://github.com/freqtrade/freqtrade) | Free; start in dry-run |

## Vibe trading and AI trading agents

| Project | ★ | Licence | Last push | What it is |
|---|---:|---|---|---|
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 119,754 | Apache-2.0 | 2026-10-27 | Simulated trading firm: analysts, bull/bear researchers that debate, trader, risk manager with veto. Research/backtest, not live. Small local models (~7B) tend to loop in the debate. |
| [OpenBB](https://github.com/openbq-org/OpenBB) | 75,018 | AGPL-3.0 ¹ | 2026-11-02 | Financial data platform; v5 ships `openbb-mcp-server` with on-demand tool discovery. Data only. (Redirects from `OpenBB-finance/OpenBB`.) |
| [virattt/ai-hedge-fund](https://github.com/virattt/ai-hedge-fund) | 64,431 | MIT | 2026-11-01 | Multi-strategy "fund" of agents with paper trading, a hash-chained ledger and an approval step before execution. |
| [anthropics/financial-services](https://github.com/anthropics/financial-services) | 40,982 | Apache-2.0 | 2026-10-28 | Anthropic's finance agent templates and plugins for Claude Code / Cowork; wires up the institutional connectors [below](#institutional-data-claude-for-financial-services). |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | 37,426 | MIT | 2026-11-01 | The reference "vibe trading" agent. See [details below](#vibe-trading-details). |
| [HKUDS/AI-Trader](https://github.com/HKUDS/AI-Trader) | 23,074 | **none** | 2026-06-11 | Live benchmark of LLMs trading NASDAQ-100, SSE-50 and crypto autonomously ([arXiv 2512.10971](https://arxiv.org/abs/2512.10971)); Polymarket paper trading. No licence file — not reusable as open source. |
| [AI4Finance-Foundation/FinGPT](https://github.com/AI4Finance-Foundation/FinGPT) | 21,510 | MIT | 2026-10-25 | Open-source financial LLMs. |
| [AI4Finance-Foundation/FinRL](https://github.com/AI4Finance-Foundation/FinRL) | 16,954 | MIT | 2026-10-25 | Reinforcement-learning trading research. |
| [NoFxAiOS/nofx](https://github.com/NoFxAiOS/nofx) | 13,188 | AGPL-3.0 | 2026-10-21 | "Agentic trading OS" built for live trading (Go + React); safety limits in code the model cannot reach; auto-protect after repeated AI failures. |
| [ValueCell-ai/valuecell](https://github.com/ValueCell-ai/valuecell) | 11,041 | Apache-2.0 | 2026-03-09 | Multi-agent finance platform (research, tracking, crypto strategy agent on OKX/Binance perps). Integrates TradingAgents and ai-hedge-fund. |
| [AI4Finance-Foundation/FinRobot](https://github.com/AI4Finance-Foundation/FinRobot) | 8,356 | Apache-2.0 | 2026-10-24 | Equity-research report agent; does not trade. |

¹ GitHub reports `NOASSERTION`; OpenBB documents AGPL-3.0.

### Alpha Arena replicas

[nof1.ai Alpha Arena](https://github.com/kukapay/awesome-alpha-arena) (LLMs trading live crypto perps from $10k each) is **not** open source. Community replicas:

| Project | ★ | Licence | Last push | Notes |
|---|---:|---|---|---|
| [wquguru/nof0](https://github.com/wquguru/nof0) | 2,754 | none | 2025-12-07 | Full reproduction in Go |
| [HammerGPT/Hyper-Alpha-Arena](https://github.com/HammerGPT/Hyper-Alpha-Arena) | 1,194 | Apache-2.0 | 2026-05-13 | Live multi-LLM trading on Hyperliquid and Binance Futures |
| [SnowingFox/open-nof1.ai](https://github.com/SnowingFox/open-nof1.ai) | 806 | none | 2026-04-01 | Real-market AI trading platform |

### Vibe-Trading details

- Install: `pip install vibe-trading-ai` → `vibe-trading` (CLI/TUI), `vibe-trading serve` (web UI), `vibe-trading-mcp` (MCP server).
- 75+ finance skills, ~478 pre-built alpha factors, backtest engines for US/global equities, China A-shares, India (NSE/BSE), Brazil (B3), crypto, futures and forex; exports to Pine Script and vnpy.
- **Keyless data:** yfinance, OKX, CCXT, AKShare, mootdx, baostock, Stooq, Eastmoney, Sina, with automatic fallback and an optional local cache (`VIBE_TRADING_DATA_CACHE`). Optional keyed: Finnhub, Alpha Vantage, Tiingo, FMP, Tushare.
- **LLM:** bring your own (OpenRouter, DeepSeek, Gemini, Groq, OpenAI, Qwen, `claude-cli`, …) or local Ollama.
- **Live trading** is opt-in: IBKR read-only, Robinhood Agentic via OAuth, with order guard, audit ledger and kill switch. v0.1.17 added paper accounts.
- ⚠️ The project states that the X account `VibeTrading_HKU`, Virtuals project 101845 and token `0x640BDBF77b6447E8b7DB7894cED84BD1c40571f4` are **not** official. Install only from the HKUDS repo or PyPI.
- Sources: [releases](https://github.com/HKUDS/Vibe-Trading/releases), [CHANGELOG](https://github.com/HKUDS/Vibe-Trading/blob/main/CHANGELOG.md), [PyPI](https://pypi.org/project/vibe-trading-ai/).

## Quant platforms and financial foundation models

| Project | ★ | Licence | Last push | What it is |
|---|---:|---|---|---|
| [microsoft/qlib](https://github.com/microsoft/qlib) | 49,930 | MIT | 2026-10-30 | AI-oriented quant research platform (data, models, backtest) |
| [vnpy/vnpy](https://github.com/vnpy/vnpy) | 46,196 | MIT | 2026-10-27 | Python quant trading platform (strong China-market connectors) |
| [shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos) | 45,706 | MIT | 2026-04-13 | Foundation model that predicts OHLCV candles as tokens (AAAI 2026) |

## Free market-data MCPs

No API key needed for the listed scope.

| Server | ★ | Licence | Last push | Data source | Notes |
|---|---:|---|---|---|---|
| [atilaahmettaner/tradingview-mcp](https://github.com/atilaahmettaner/tradingview-mcp) | 5,190 | MIT | 2026-10-29 | TradingView screener | 39 tools: screeners, multi-timeframe TA, backtests, sentiment |
| [wshobson/maverick-mcp](https://github.com/wshobson/maverick-mcp) | 716 | MIT | 2026-10-31 | Yahoo (`yfinance`), finviz | 38 core tools + optional backtesting extra. Install from Git, not the unrelated PyPI name. |
| [stefanoamorelli/sec-edgar-mcp](https://github.com/stefanoamorelli/sec-edgar-mcp) | 383 | AGPL-3.0 | 2026-11-01 | SEC EDGAR (official) | Filings, financial statements, insider trades |
| [Alex2Yang97/yahoo-finance-mcp](https://github.com/Alex2Yang97/yahoo-finance-mcp) | 365 | MIT | 2026-09-19 | Yahoo | Prices, fundamentals, option chains, news |
| [narumiruna/yfinance-mcp](https://github.com/narumiruna/yfinance-mcp) | 205 | MIT | 2026-11-01 | Yahoo | Minimal |
| [doggybee/mcp-server-ccxt](https://github.com/doggybee/mcp-server-ccxt) | 145 | MIT | 2025-06-03 | Exchange public APIs via CCXT | Trading needs exchange keys. Stale. |
| [vdalhambra/financekit-mcp](https://github.com/vdalhambra/financekit-mcp) | 9 | MIT | 2026-04-17 | Yahoo, CoinGecko | Plain-English signal summaries |
| [yyordanov-tradu/stock-scanner-mcp](https://github.com/yyordanov-tradu/stock-scanner-mcp) | 8 | MIT | 2026-10-26 | TradingView screener and others | 49 keyless tools |
| [daniel3303/stock-market-mcp-server](https://github.com/daniel3303/stock-market-mcp-server) | 7 | MIT | 2026-10-19 | Multiple | 64 tools self-hosted; hosted plan 100 req/day |
| [safrano9999/fin-data-mcp](https://github.com/safrano9999/fin-data-mcp) | 0 | MIT | 2026-10-25 | Yahoo, Cboe + 13 more | 83 keyless tools — widest claimed coverage, but brand new and unproven |
| [leogue/StockMCP](https://github.com/leogue/StockMCP) | 4 | none | 2025-08-27 | Yahoo | Also offers a hosted endpoint |

Official endpoints with a keyless tier:

| Provider | Endpoint | Keyless scope |
|---|---|---|
| CoinGecko | `https://mcp.api.coingecko.com/mcp` ([docs](https://docs.coingecko.com/docs/mcp-server)) | Public crypto market data (beta) |
| Glassnode | `https://mcp.glassnode.com` ([list](https://github.com/hive-intel/awesome-crypto-mcp-servers)) | Last 30 days of on-chain metrics |
| Gate | `api.gatemcp.ai/mcp` ([repo](https://github.com/gate/gate-mcp)) | Market data, `/mcp/info`, `/mcp/news` |
| OKX | `okx-trade-mcp --modules market` ([repo](https://github.com/okx/agent-trade-kit)) | Market data |
| Bybit | [trading-mcp](https://github.com/bybit-exchange/trading-mcp) read-only mode | Market data |

## Official broker MCPs

| Broker | Repo / endpoint | Assets | Notes |
|---|---|---|---|
| Alpaca | [alpacahq/alpaca-mcp-server](https://github.com/alpacahq/alpaca-mcp-server) (★1,054, MIT) | US stocks, ETFs, options, crypto | Paper by default. [V2](https://alpaca.markets/blog/alpaca-launches-mcp-server-v2/): 61 tools, toolset filtering |
| Interactive Brokers | `api.ibkr.com/v1/api/mcp-public` ([press](https://www.interactivebrokers.com/en/index.php?f=78687)) | Global | IBKR login, one account approved |
| Robinhood | `agent.robinhood.com/mcp/trading` ([review](https://www.finder.com/stock-trading/robinhood-agentic-accounts)) | US stocks, crypto; options rolling out | Beta since 2026-05-27. Orders only in a dedicated agentic account. US only. |
| tastytrade | [tastytrade/tastytrade-mcp](https://github.com/tastytrade/tastytrade-mcp) (★36) | US stocks, options | Self-hosted. Dry-run-gated orders; `TASTYTRADE_READ_ONLY=1` |
| Webull | `api.webull.com/mcp` + [webull-inc/webull-openapi-mcp](https://github.com/webull-inc/webull-openapi-mcp) (★30, Apache-2.0) | Equities, options, futures, crypto | Cloud MCP prepares trades that need customer confirmation; local server can place orders ([analysis](https://vorplabs.com/agent-tools/webull-mcp)) |
| Public.com | `mcp.public.com/mcp` ([directory](https://github.com/mphinance/awesome-broker-mcp)) | Stocks, ETFs, options, crypto, bonds | OAuth, preflight checks. No paper mode. |
| moomoo / Futu | `mcp.moomoo.com/mcp` ([directory](https://github.com/mphinance/awesome-broker-mcp)) | Multi-market | Browser sign-in; trade scope + trade password for orders |
| Tradier | Hosted ([docs](https://docs.tradier.com/docs/tradier-mcp)) | US stocks, options | Personal API token |
| TradeStation | Hosted ([comparison](https://fensory.com/best/mcp-servers-for-trading)) | Stocks, options, futures | $10k minimum balance |
| Zerodha (India) | `mcp.kite.trade/mcp` + [zerodha/kite-mcp-server](https://github.com/zerodha/kite-mcp-server) (★329, MIT) | NSE/BSE | Hosted is read-only (except GTT); self-host for full order tools |
| Dhan (India) | `mcp.dhan.co/mcp` ([comparison](https://quantlabin.substack.com/p/every-indian-broker-has-an-mcp-now)) | NSE/BSE | Each order needs confirmation; LIMIT by default |
| Upstox, Groww (India) | ([comparison](https://quantlabin.substack.com/p/every-indian-broker-has-an-mcp-now)) | NSE/BSE | Upstox read-only; Groww supports orders |
| Korea Investment & Securities | [koreainvestment/open-trading-api](https://github.com/koreainvestment/open-trading-api) (★1,658) | KRX | Official SDK with trading MCP, strategy builder, backtester |

**No official MCP** (as of the [QuantVPS check, 2026-10-10](https://www.quantvps.com/blog/agentic-trading-brokers)): Fidelity, Charles Schwab, E\*TRADE, Merrill, Ally. Community Schwab server: [k1xme/schwab-mcp](https://github.com/k1xme/schwab-mcp) (★0, no licence).

## Official crypto exchange MCPs

| Exchange | Repo / endpoint | Notes |
|---|---|---|
| OKX | [okx/agent-trade-kit](https://github.com/okx/agent-trade-kit) (★498, MIT) + [okx/agent-skills](https://github.com/okx/agent-skills) (★201) | Spot, swap, futures, options, grid bots; `--read-only` flag. Many look-alike forks exist — use the `okx/` org only. |
| Kraken | [krakenfx/kraken-cli](https://github.com/krakenfx/kraken-cli) (★792, MIT) | CLI with built-in MCP; crypto, tokenized stocks, forex, futures. Read-only for live funds by default. |
| Bitget | [Bitget-AI/agent_hub](https://github.com/Bitget-AI/agent_hub) (★234, MIT) | CLI, MCP (`npx -y bitget-mcp-server`), SDK, skills |
| Gate | [gate/gate-mcp](https://github.com/gate/gate-mcp) (★44, MIT) | Hosted; trading behind scoped OAuth2 (no key in a file) |
| Bybit | [bybit-exchange/trading-mcp](https://github.com/bybit-exchange/trading-mcp) (★43, MIT) | 382 tools on the V5 API |
| Binance | `agent.binance.com/mcp/agentic` ([guide](https://essamamdani.com/blog/binance-agent-os-mcp-developer-guide-2026)) | Agent OS, Aug 2026. Separate agentic sub-account, no withdrawal scope. |
| Coinbase | [Coinbase for Agents](https://www.coinbase.com/blog/coinbase-for-agents) | June 2026. Crypto, US futures, S&P 500 equities. OAuth, isolated portfolio. |
| Injective | [InjectiveLabs/mcp-server](https://github.com/InjectiveLabs/mcp-server) (★9) | On-chain perpetuals |
| Hyperliquid | **No official server** | Community servers (e.g. [edkdev/hyperliquid-mcp](https://github.com/edkdev/hyperliquid-mcp), ★24) often store a raw private key in a file — use an agent wallet that cannot withdraw. |
| KuCoin | **No official server** | Community only |

## Forex and CFD

| Platform | Repo / endpoint | Notes |
|---|---|---|
| cTrader (Spotware) | Official remote + local MCP ([docs](https://help.ctrader.com/ctrader-ai-agent-connect/)) | Remote via cTrader Web token; local server trades with optional per-order confirmation |
| eToro | Official `mcp.public-api.etoro.com` ([blog](https://builders.etoro.com/blog/vibe-coding-with-etoro-mcp)) | Exposes the full API spec; scoped by your user key. Community: [slemos/etoro-mcp-server](https://github.com/slemos/etoro-mcp-server) (demo/read-only by default) |
| MetaTrader 5 | [Qoyyuum/mcp-metatrader5-server](https://github.com/Qoyyuum/mcp-metatrader5-server) (★238), [mt5-mcp](https://pypi.org/project/mt5-mcp/) | Community; Windows-only (MT5 Python SDK) |
| OANDA | [florinel-chis/oanda-mcp](https://github.com/florinel-chis/oanda-mcp) (★2, MIT) | Community; practice env by default, trading hidden unless enabled |
| Saxo | [sigvardt/saxo-bank-mcp](https://github.com/sigvardt/saxo-bank-mcp) (★0) | Community; SIM-first, live writes off by default |
| IG | [kea0811/ig-trading-mcp](https://github.com/kea0811/ig-trading-mcp) (★8) | Community; 21 tools, Lightstreamer prices |

## Keyed market-data MCPs

| Provider | Repo / endpoint | Notes |
|---|---|---|
| Financial Datasets | [financial-datasets/mcp-server](https://github.com/financial-datasets/mcp-server) (★2,315, MIT) + `mcp.financialdatasets.ai` | Official. Statements, prices, news. Hosted version uses OAuth. |
| Massive (formerly Polygon.io) | [massive-com/mcp_massive](https://github.com/massive-com/mcp_massive) (★399, MIT) | Official. Tick-level stocks, options, FX, crypto. |
| Twelve Data | [twelvedata/mcp](https://github.com/twelvedata/mcp) (★85) + `mcp.twelvedata.com/mcp` | Official, early-stage; free plan available |
| Financial Modeling Prep | [Hosted MCP docs](https://site.financialmodelingprep.com/developer/docs/mcp-server) | Official; free plan 250 calls/day |
| EODHD | `mcp.eodhd.com/v2/mcp` ([docs](https://eodhd.com/financial-apis/mcp-server-for-financial-data-by-eodhd)) | Official; OAuth 2.1 (v2) or key in URL (v1) |
| Alpha Vantage | `mcp.alphavantage.co` / [calvernaz/alphavantage](https://github.com/calvernaz/alphavantage) (★74) | Free tier 25 req/day |
| Tiingo | [major7apps/tiingo-mcp](https://github.com/major7apps/tiingo-mcp) (★11, MIT) | Community; IEX-based real-time |
| Finnhub | ([comparison](https://sentisense.ai/blog/best-mcp-servers-market-data-2026/)) | Sources disagree on whether an official server exists |
| FRED (open source) | [stefanoamorelli/fred-mcp-server](https://github.com/stefanoamorelli/fred-mcp-server) (★130, AGPL-3.0), [shanehull/fred-mcp](https://github.com/shanehull/fred-mcp) | Need a free FRED API key (the official connector does not) |

## Crypto analytics, on-chain and sentiment MCPs

All official, hosted, and mostly paid beyond a free tier. Endpoints per [hive-intel/awesome-crypto-mcp-servers](https://github.com/hive-intel/awesome-crypto-mcp-servers) and vendor docs.

| Provider | Endpoint | Covers |
|---|---|---|
| CoinMarketCap | ([connector](https://glama.ai/mcp/connectors/com.coinmarketcap/coinmarketcap)) | Quotes, TA, on-chain, narratives, news |
| Dune | Official remote | DuneSQL queries, dashboards |
| Nansen | Official remote | Smart-money labels, wallet flows, 25+ chains |
| Glassnode | `mcp.glassnode.com` | On-chain metrics (30 days free) |
| Santiment | `api.santiment.net/mcp` | Social + on-chain metrics, OAuth |
| LunarCrush | `lunarcrush.ai/mcp` | Social sentiment; free tier 100 req/day |
| Messari | `mcp.messari.io/mcp` | Research, unlocks, fundraising; sales-gated |
| DefiLlama | Unconfirmed (one community list only) | TVL, yields |

## Institutional data (Claude for Financial Services)

Enterprise connectors listed in [anthropics/financial-services](https://github.com/anthropics/financial-services); each needs a subscription with the provider.

| Provider | MCP endpoint |
|---|---|
| FactSet | `https://mcp.factset.com/mcp` |
| S&P Global (Capital IQ, via Kensho) | `https://kfinance.kensho.com/integrations/mcp` |
| LSEG | `https://api.analytics.lseg.com/lfa/mcp` |
| Morningstar | `https://mcp.morningstar.com/mcp` |
| Daloopa | `https://mcp.daloopa.com/server/mcp` |
| Also listed | Moody's, MT Newswires, Aiera, PitchBook, Chronograph, MSCI |

## Prediction markets

Neither Kalshi nor Polymarket runs a first-party MCP server.

| Server | Notes |
|---|---|
| [PMXT](https://www.pmxt.dev/mcp) | Hosted unified API; can place trades on Polymarket, Kalshi and others |
| [DepthFeed](https://depthfeed.com/mcp) | Order-book data for Polymarket, Kalshi, Limitless; limited keyless access |
| [huntbuilds/mcp-prediction-markets](https://glama.ai/mcp/servers/huntbuilds/mcp-prediction-markets) | Search, odds, arbitrage; no keys |
| [Viprasol-Tech/marketsmith](https://github.com/Viprasol-Tech/marketsmith) | EV and Kelly sizing; live feeds still on the roadmap |

## Research, backtesting and charting MCPs

| Tool | Repo / endpoint | Notes |
|---|---|---|
| QuantConnect | [QuantConnect/mcp-server](https://github.com/QuantConnect/mcp-server) (★79, Apache-2.0) | Official. Create projects, backtest, deploy live algorithms. |
| TradingView (official) | ([roundup](https://github.com/Ricosworks1/blockchain-payment-flow-analysis/releases/tag/market-update-exchanges-ship-ai-agent-mcp-infrastructure-oct-2026)) | Public beta Sept 2026, paid plans only |
| Trading Central | ([press](https://www.bnnbloomberg.ca/press-releases/2026/09/21/trading-central-launches-mcp-server-to-power-financial-ai-agents-chatbots-with-trusted-research/)) | Commercial research MCP for brokerages |
| Paper | [paperinvest/mcp-server](https://github.com/paperinvest/mcp-server) (★24, MIT) | Hosted paper-trading platform; API key |
| Open Paper Trading | [Open-Agent-Tools/open-paper-trading-mcp](https://github.com/Open-Agent-Tools/open-paper-trading-mcp) (★17) | Self-hosted simulator |
| MCP Trader | [wshobson/mcp-trader](https://github.com/wshobson/mcp-trader) (★273) | **Archived** — superseded by MaverickMCP |

## Trading engines, bots and backtesting libraries

| Project | ★ | Licence | Last push | Best for |
|---|---:|---|---|---|
| [freqtrade/freqtrade](https://github.com/freqtrade/freqtrade) | 56,310 | GPL-3.0 | 2026-11-02 | Signal-driven crypto bots; Hyperopt; FreqAI |
| [nautechsystems/nautilus_trader](https://github.com/nautechsystems/nautilus_trader) | 31,157 | LGPL-3.0 | 2026-11-02 | Production-grade, Rust core, deterministic simulation |
| [mementum/backtrader](https://github.com/mementum/backtrader) | 23,638 | GPL-3.0 | **2024-08-19** | Classic Python backtester — no longer maintained |
| [QuantConnect/Lean](https://github.com/QuantConnect/Lean) | 22,343 | Apache-2.0 | 2026-10-30 | Multi-asset research → live |
| [hummingbot/hummingbot](https://github.com/hummingbot/hummingbot) | 20,910 | Apache-2.0 | 2026-10-20 | Market making, CEX/DEX arbitrage |
| [polakowo/vectorbt](https://github.com/polakowo/vectorbt) | 9,636 | Apache-2.0 + Commons Clause | 2026-10-28 | Very fast vectorised backtests; **not free for commercial use** |
| [kernc/backtesting.py](https://github.com/kernc/backtesting.py) | 9,176 | AGPL-3.0 | 2026-08-05 | Lightweight Python backtester |
| [jesse-ai/jesse](https://github.com/jesse-ai/jesse) | 8,757 | MIT | 2026-10-31 | Crypto bot framework (live plugin is commercial) |
| [Drakkar-Software/OctoBot](https://github.com/Drakkar-Software/OctoBot) | 6,884 | GPL-3.0 | 2026-10-27 | Crypto bot with web UI: AI, grid, DCA, TradingView signals |
| [stefan-jansen/zipline-reloaded](https://github.com/stefan-jansen/zipline-reloaded) | 1,996 | Apache-2.0 | 2026-11-01 | Maintained fork of Quantopian's Zipline |

## Where the free data actually comes from

| Source | Status | Used by |
|---|---|---|
| Yahoo Finance via `yfinance` | **Unofficial** — can break, rate-limit or lag | MaverickMCP, yahoo-finance-mcp, yfinance-mcp, StockMCP, financekit, Vibe-Trading, fin-data-mcp |
| TradingView screener, finviz | Unofficial web endpoints | tradingview-mcp, stock-scanner-mcp, MaverickMCP |
| SEC EDGAR | Official, public | sec-edgar-mcp |
| FRED (St. Louis Fed) | Official | FRED connector and servers |
| CoinGecko, OKX, Gate, Bybit, Binance, Cboe public APIs | Official public endpoints | CoinGecko MCP, exchange MCPs, Vibe-Trading, CCXT servers |
| AKShare, mootdx, baostock | Community wrappers (mainly China markets) | Vibe-Trading |

Free data is fine for research and prototypes. It is not production-grade for real-money decisions.

## Safety checklist

1. Start **read-only or paper**. Move to live only with a small, dedicated sub-account.
2. **Never grant withdrawal scope.** Prefer brokers that isolate the agent (Robinhood agentic account, Binance agentic sub-account, Coinbase isolated portfolio).
3. Prefer **OAuth with scopes** over API keys in files; never put a raw wallet private key in a config file.
4. Require **human approval** per order where the server supports it (tastytrade dry-run, Dhan, cTrader, Webull Cloud, ai-hedge-fund approval step).
5. Install from the **official repo only** — popular projects (OKX, Vibe-Trading) have many look-alike forks and token scams.
6. Read the code of community servers before giving them credentials. MCP servers are exposed to poisoned tool descriptions and prompt injection.

## Related lists

| List | ★ | Focus |
|---|---:|---|
| [paperswithbacktest/awesome-systematic-trading](https://github.com/paperswithbacktest/awesome-systematic-trading) | 15,134 | Systematic trading libraries, strategies, books |
| [LLMQuant/awesome-trading-agents](https://github.com/LLMQuant/awesome-trading-agents) | 966 | LLM trading agents, MCP servers, skills |
| [BlockRunAI/awesome-finance-mcp](https://github.com/BlockRunAI/awesome-finance-mcp) | 251 | Finance MCP servers |
| [kukapay/awesome-alpha-arena](https://github.com/kukapay/awesome-alpha-arena) | 31 | Alpha Arena replicas |
| [hive-intel/awesome-crypto-mcp-servers](https://github.com/hive-intel/awesome-crypto-mcp-servers) | 12 | Crypto / Web3 MCP servers |
| [narekgevorgyan/crypto-mcp-servers](https://github.com/narekgevorgyan/crypto-mcp-servers) | 12 | 100+ crypto MCP servers |
| [mphinance/awesome-broker-mcp](https://github.com/mphinance/awesome-broker-mcp) | 1 | Which brokers an AI can actually trade through |

## Methodology

- Compiled from ~45 web searches and vendor docs between 2026-10-27 and 2026-11-02, then cross-checked against the related lists above for gaps.
- GitHub numbers were pulled from `api.github.com/repos/{owner}/{repo}` on 2026-11-02. Rows without a star count are hosted services with no public repo.
- Many "best MCP" roundups are published by vendors that rank their own product; those were used only for facts that could be cross-checked, not for rankings.
- Corrections welcome — open an issue or PR with a source link.

## Licence

[MIT](LICENSE)
