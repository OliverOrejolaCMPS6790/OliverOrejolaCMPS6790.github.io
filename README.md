# Cointegration and Causality: Statistical Analysis of Apple’s Supply Chain
## CMPS 6790 Fall 2023 Project Website
Data Science: CMPS 6790, Fall 2023

[A link to the page can be found here](https://oliverorejolacmps6790.github.io)

### Summary
Apple's iPhone relies on components supplied by a diverse array of companies, including Qualcomm, which provides 5G modems for Apple's iPhones, and Intel, a major supplier of microprocessors (CPUs) for certain Apple devices. Given this extensive supply chain involvement, a natural expectation arises regarding the potential statistical relationships between Apple's stock price and those of the companies within its product supply chain.<br>
&nbsp;&nbsp;&nbsp;&nbsp; However, establishing and understanding such financial relationships poses challenges. Many machine learning models and algorithms used for predicting stock and commodity prices rely on correlations between variables, often employing methods like linear regression. Yet, relying solely on correlation can be perilous, as Yule's 1926 study highlighted. Particularly in the case of non-stationary time-series distributions, estimating the correlation coefficient can often lead to [spurious](https://en.wikipedia.org/wiki/Spurious_relationship) relationships (read more about spurious correlation for non-stationary processes [here](https://www.jstor.org/stable/2246135)). Namely, with high-probability, the magnitude of the estimated correlation coeffieicnt of two independent non-stationary stochastic processes  is close to 1. To clairfy, we say a processes, $X(t)$, is stationary (wide sense stationary) if it's mean variance does not change over time.<br>
&nbsp;&nbsp;&nbsp;&nbsp;In light of this, [Robert Engle and Clive Granger (1987)](https://www.jstor.org/stable/1913236) introduced the concept of [cointegration](https://en.wikipedia.org/wiki/Cointegration). Loosely speaking, we say two non-stationary stochastic processes are cointegrated if there exists a linear combination of them which is stationary. Specifically, let $X(t)$ and $Y(t)$ be two non-stationary processes. We say $X(t)$ and $Y(t)$ are cointegrated if there exists constants $\alpha$ and $\beta$ such that the process $\{Z(t)\}_{t\in\mathbb{R}}$, defined as

$$Z(t) := \alpha X(t) + \beta Y(t) $$
is stationary.<br>
&nbsp;&nbsp;&nbsp;&nbsp; Outside of the theoritical shortcomings of the correlation, cointegration provides an intuitive model for the relationship between two non-stationary processes. This is structure is often taken advantage of in finance in the for of a trading scheme known as [trading pairs](https://en.wikipedia.org/wiki/Pairs_trade). A strategy which is based on the mean reversion pricnciple of the stationary process $Z(t)$, where $X(t)$ and $Y(t)$ may be two asset prices. The cointegraiton structure is additionally suggestive of a form of causal structure. Cointegration is often used in conjunction with [Granger Causality](https://en.wikipedia.org/wiki/Granger_causality) tests. When variables are cointegrated, Granger causality tests can provide insights into the direction of causality between them. Here a "causal effect" means that $X(t)$ has predictive power for $Y(t)$. Inparticular, an [autoregrssive](https://en.wikipedia.org/wiki/Autoregressive_model) (AR) model for $Y(t)$ which includes $X(t)$ lag terms is more predictive than an AR without $X(t)$ lag terms.

&nbsp;&nbsp;&nbsp;&nbsp; In this project we studying conintegration and Grainger causality among Apple (AAPL) stock and 
[8  major American companies tied to the Apple supply chain](https://www.investopedia.com/articles/investing/090315/10-major-companies-tied-apple-supply-chain.asp#:~:text=One%20of%20the%20largest%20suppliers,popular%20products%2C%20including%20the%20iPhone.).
* 3M (MMM) 
* Broadcom (AVGO) 
* Qualcomm (QCOM) 
* Intel (INTC) 
* Jabil Curcits (JBL)
* On (ON) 
* Micron (MU) 
* Texas Instruments (TXN) 

We demonstrate that for certain time intervals statistically signficant cointegration occurs. In addition, we show that there is indeed Grainger causality.

**n.b.** The abbreviation in parenthesis is refered to as a ticker. The ticker is a short hand name for the company on a stock exchange. All companies listed are traded on the New York Stock Exchange.

## Project Data Set

For this project we will be loading in historical stock market data for each of the companies listed above. Our data consists of historical stock market data from 1/1/2018 to 10/31/2023. The data is taken using the  [yahoo finanace api](https://pypi.org/project/yfinance/). For simplicity in our investigation of conintegraiton and causality, we will only look at the value of the stock based on opening price for each day.

#### Techniques Used
  * [statsmodels](https://www.statsmodels.org/stable/index.html)
    * [Ordinary Least Squares](https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.OLS.html)   
    * [statsmodels.tsa](https://www.statsmodels.org/stable/tsa.html)
      * [Augmented Dickey–Fuller test](https://www.statsmodels.org/dev/generated/statsmodels.tsa.stattools.adfuller.html)
      * [Kwiatkowski–Phillips–Schmidt–Shin test](https://www.statsmodels.org/stable/generated/statsmodels.tsa.stattools.kpss.html)
      * [Granger Causality Test](https://www.statsmodels.org/stable/generated/statsmodels.tsa.stattools.grangercausalitytests.html)
  * Engle-Granger Two Step Method
