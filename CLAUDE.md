# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Streamlit dashboard showing the 2025 stock performance of four Brazilian equities: Petrobras (PETR4), Vale (VALE3), Itaú (ITUB4), and Banco do Brasil (BBAS3).

## Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run the app
streamlit run acoes_2025.py
```

## Architecture

Single-file app (`acoes_2025.py`):

- **Data loading** — `carregar_dados_yfinance()` fetches daily closing prices for 2025 from Yahoo Finance using tickers with the `.SA` suffix (e.g. `PETR4.SA`). Results are cached with `@st.cache_data`. If the download fails, a hardcoded monthly price table (`DADOS_2025`) is used as fallback.
- **Visualization** — Three sections rendered with Plotly via `st.plotly_chart`: `st.metric` cards (one per stock), a normalized performance line chart (base 100), and a horizontal bar chart for % return comparison.
- **Interactivity** — Sidebar checkboxes let the user select which stocks to display; all charts and metrics update reactively.

## GitHub

Repositório: https://github.com/cesarawi/acoes-brasileiras-2025

Todo arquivo editado ou criado pelo Claude é automaticamente commitado e publicado no GitHub via hook `PostToolUse` configurado em `.claude/settings.json`. O hook executa `git add -A && git commit -m "auto: update <arquivo>" && git push origin main` após cada operação de escrita.

Para commitar manualmente:
```bash
cd D:/claude
git add -A
git commit -m "mensagem"
git push origin main
```

## Key notes

- yfinance 1.2.0+ is required — earlier versions fail to resolve Brazilian tickers.
- The `Close` column from yfinance 1.2.0 returns a multi-level DataFrame; the code flattens it with `iloc[:, 0]`.
- Python 3.11.0 (see `.python-version`).
