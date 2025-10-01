---
share: true
---
2025-10-01  10:51
Tags:[[Mentol Models|Mentol Models]]
# [Mean Reversion](https://corporatefinanceinstitute.com/resources/career-map/sell-side/capital-markets/mean-reversion/#:~:text=Mean%20reversion%20is%20a%20theory,within%20a%20set%20of%20data.)

### What is Mean Reversion?
>Mean reversion is a theory implying that asset prices and historical returns gradually move towards the long-term mean, which can be based on the economy, industry, or average return within a set of data.

### Trading with Mean Reversion
>Applying that knowledge, investors are capable of measuring and determining when to buy under the mean and sell above it. Mean reversion is also used in [options pricing](https://corporatefinanceinstitute.com/resources/derivatives/option-pricing-models/) to better determine how an asset’s volatility fluctuates along with its long-term average.
>
>Investors employ mean reversion strategies to capitalize on asset prices that have deviated **significantly** from their historical mean.

I would say **significantly** is the heighlight.
### How Catalysts Affect Mean Reversion
>It is important to recognize that unexpected highs or lows can ultimately imply a shift in the nature of the stock, caused by events such as positive or negative news.
>
>Generally, returns of normal patterns are not always guaranteed, but it is indeed still possible for assets to experience mean reversion in the most extreme circumstances. Nonetheless, much like any event, it is difficult to fully determine how market activity for securities will be affected by the news.

### Random Walk

>Instead of reverting back to the mean, stock prices may lead to a random walk post-shock. A random walk is a process when prices do not return to previous levels, nor do they gradually move towards the mean. For example, an increase in the momentum of the stock may lead to a greater deviation from the mean.

# [Musings on Markets](https://aswathdamodaran.blogspot.com/2016/08/mean-reversion-gravitational-super.html?utm_source=chatgpt.com)

### Mean Reversion: Basis and Push Back
>The notion of mean reversion is widely held and deeply adhered to not just in many disciplines but in every day life. In sports, whether it be baseball, basketball, football or soccer, we use mean reversion to explain why hot (and cold) streaks end. In investments, it is an even stronger force explaining why funds and investors that fly high come back to earth and why strategies that deliver above-average returns are  unable to sustain that momentum.

>At the risk of over generalization, much of market timing is built on time series mean reversion, whereas the bulk of stock selection is on the basis of cross sectional mean reversion. While both may draw their inspiration from the same intuition, they do make different underlying assumptions and may pose different dangers for investors.


🕰️ 1. Time-series mean reversion (Market Timing)

- **What it means**: Looking at how one variable (say, the market P/E ratio, or interest rates) moves over time, and betting it will go back to its historical average.
    
- **Example**:
    
    - If the S&P 500 CAPE ratio is way above its long-term mean, you might predict a correction.
        
    - If inflation spikes unusually high, you expect it to come down toward its historical level.
        
- **Underlying assumption**: The past average is a “true anchor,” and forces (policy, competition, investor psychology) will pull the series back.
    
- **Danger**: Sometimes the world _changes structurally_. For example, tech companies really did earn higher margins after the internet scaled — waiting for “mean reversion” could leave you out of decades of growth.
    

👉 This is what people try when they “time the market” by saying: _“The market is too high, it must fall soon.”_

---

📊 2. Cross-sectional mean reversion (Stock Selection)

- **What it means**: Looking at differences **across companies** at one point in time, assuming extremes won’t last.
    
- **Example**:
    
    - A company with unusually high profit margins vs peers → assume competition will erode those margins.
        
    - A company with unusually poor returns → assume survival pressure or recovery will push it closer to peer averages.
        
- **Underlying assumption**: Industries are competitive, and competitive advantages erode; no company stays extreme forever.
    
- **Danger**: Some companies _do_ have durable moats (Apple, Coca-Cola, McDonald’s). Their high returns persist for decades, and waiting for mean reversion makes you underestimate them.
    

👉 This is what many “value investors” try when they say: _“This stock is too cheap compared to peers; eventually it will revert.”_

---

这个真的需要辩证看待 首先Cross-sectional mean reversion我就觉得不行 均值回归很难在长牛市场实现 但是你又怎么知道这是长牛市场呢？

### The Fundamental Critique
>The first is _aging_, with the argument easiest to make with individual companies and more difficult with entire markets. As companies move through the life cycle, you will generally see the numbers for the company reflect that aging, rather moving to historic norms. That is especially true for growth rates, with growth rates decreasing as a company scales up and becomes more mature, but it is also true of both other operating numbers (margins, costs of capital) as well as pricing metrics (price earnings ratios and EV multiples). While markets, composed of portfolios of companies, are less susceptible to aging, you could argue that aging equity markets (the US, Japan and Europe) will exhibit different characteristics than they did when were younger and more vibrant.

>- The second is _technology and industry structure_, shaking up both the product market structure and creating challenges for accountants. This is true clearly at the company level, as is the case with retailing, where Amazon's entry and subsequent growth has laid waste to historic norms for this sector, bringing down operating margins and changing reinvestment patterns. It is also true at the market level, where an increasing proportion of the equity market (say, the S&P 500) are service and technology stocks and the accounting for expenses in these sectors (with many capital expenses being treated as operating expenses) creating questions about whether the E in the PE for the S&P 500 is even comparable over time.

>- The third is _changes in consumer and investor preferences_, with the first affecting the numbers in product markets and the latter in financial markets. For instance, there is an argument to be made that the surge in index funds has altered how stocks are priced today, as opposed to two or three decades ago.

>Looking at this data, at least, the evidence seems strong that a high CAPE today goes with lower stock returns in future periods, with the mean reversion becoming stronger for longer time periods.
>In fact, if you are one of those who lives and dies by statistics, using today's CAPE of 27.27 in this regression will yield a predicted annualized return of 4.30% on stocks for the next 10 years:  

Expected annualized return in next 10 years = 16.24% - 0.0044 (27.27) = 4.30%
16年的文章 但其实一直在长牛 如果空仓那错过了多少

>The CAPE's timing payoff is greater when it is used as a buying metric than as a selling metric. In fact, you make a positive payoff from using a low CAPE as a buying indicator over the entire period but using it is a signal of over priced markets costs you money in both time period.
>有意思哈

### Conclusion
>Both in academia and in practice, I see more and more use of statistical significance as proof that you can beat markets and my reason devising and testing out market timing strategies with CAPE were not meant to be an assault on CAPE but more a cautionary note that statistical correlation is not cash in the bank. **This may also explain why there are so many ways to beat the market, on paper, and so few seem to be able to deliver those magical excess returns, in practice.**

反正我觉得不适合只用这一种工具 但可以参考 尤其在市场恐慌时 我觉得是可以利用它大量买入但卖出确实很难去选择
