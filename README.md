# trading---Value-Momentum
We will use Fama-Macbeth (FM) Regression to estimate stocks's future return, and use these forcasts to form a trading strategy.

Procedure:

1. At the beginning of year 0 (e.g. beginning of 2000) ,  only select top 50% market cap stocks by looking at their previous year (e.g. end of 1999)'s market cap. We use lagged market cap to avoid look-ahead bias.
2. Run FM Regression on the last 30 year data (1971-2000).

More specifically, the FM regression: 
    
    R @t = b0 + b1* E/P @t-1 + b2* VOL @t-1 + b3* MOM @t-1, where MOM = sum of the first 11 month returns in the past 13 months. 

- We use E/P ratio because its a metric for "value"; a low "value" generally implies a higher future return.
- We use volume as a proxy of liquidity. A high liquidity stocks can be a signal of quality, and a high quality stock is usually associate with high returns.
- Momentum as a technical indicator. The highest momentum stock is expected to be a winner, and thus is it expected to persist in future performance.

3. Use the model to predict each stock's monthly returns in next year (e.g. 2001), so each year has 12 forecasts for each stock.
4. Split the stocks into 5 groups using the forecasted monthly returns.
5. Long only the highest forecasted return group. Components in the portfolio are adjusted every month.
6. At the beginning of next year, repeat step 1 to 2 but using 1972-2001 data to update the model, and so on.

Detailed explanation:

We will only look at the stocks belong to the top 50% market value since low market cap stocks are more likely to associate with bad quality than high cap stocks, so first we want to exclude all the stocks in low 50% perceniile for each month (using lagged MV). In the beginning of each year, we will apply FM regression to the past 30 year stock data to generate coefficients, b0, b1, b2. And then we will use the coefficients to estimate the monthly return for each stock for the next year. For example, we will use the 1971 to 2000 data to build our model and use the model to forecast the monthly return of stocks in 2001. We will then seperate stocks into 5 groups based on the level of its forcasted return and long only the highest forecasted return group (group 5) as an equally weighted portfolio. In the beginning of the next year, we will repeat the same FM regression, compute the new coefficients, apply the the computed coefficients to monthly data to generate forecasted monthly return, and re-select stocks. The back-test is conducted from 2001 to 2021.
