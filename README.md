# Gold vs. Interest — Investment Modeling Tools

Two Streamlit apps that model investment returns, built while studying Mathematics Engineering at Istanbul Technical University.

**Live demos:** [Gold vs. deposit interest](https://altin-faiz-kiyaslama-eew6qjzabgbehrjjer4msi.streamlit.app/) · [Continuous compound interest](https://altin-faiz-kiyaslama-7csux5zjkw9sbehrkq6sve.streamlit.app/)

## 1. Historical comparison — `altin_vs_faiz.py`

[Open the app](https://altin-faiz-kiyaslama-eew6qjzabgbehrjjer4msi.streamlit.app/)

Answers a concrete question: if you had invested in gold instead of a deposit account, where would you be today?

The app pulls real historical prices from Yahoo Finance — gold futures (`GC=F`) and USD/TRY (`TRY=X`) — and derives the gram gold price in Turkish lira. It then runs a day-by-day simulation of two portfolios side by side:

- **Gold:** the initial capital buys grams at the starting price; every month a fixed amount buys more grams at that day's price.
- **Deposit:** the same cash flows grow at a daily compounded rate derived from the annual interest rate you set.

Both are plotted against the total cash actually invested, so the return is separated from the contributions.

**Inputs:** date range, initial capital, monthly contribution, average annual deposit rate.

## 2. Continuous compound interest — `surekli_bilesik_faiz_hesaplamasi.py`

[Open the app](https://altin-faiz-kiyaslama-7csux5zjkw9sbehrkq6sve.streamlit.app/)

Models an investment under continuous compounding with a steady cash flow, described by the differential equation

```
dS/dt = rS + k
```

The app uses the analytical solution

```
S(t) = S₀·e^(rt) + (k/r)·(e^(rt) − 1)
```

and handles the `r = 0` case separately, where the balance grows linearly. Rates and cash flows can be entered on a monthly or annual basis; the app converts between them and shows both.

**Inputs:** initial capital, interest rate, cash flow, term.

## Running locally

```bash
pip install -r requirements.txt
streamlit run altin_vs_faiz.py
```

Replace the filename to run the other app.

## Built with

Python · Streamlit · yfinance · pandas · NumPy · Matplotlib

## Notes

Both apps are hosted on Streamlit Community Cloud, which puts them to sleep after a period of inactivity — the first visit may take a few seconds to wake.

The historical app depends on Yahoo Finance being reachable; if the expected tickers don't come back, it reports the problem instead of failing silently. Gram gold is derived from the ounce price and the exchange rate rather than read directly, so it approximates the local market price without spreads or premiums.
