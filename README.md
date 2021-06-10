# Tradingview_Indicators
Modified and preferred indicators(pine in tradingview)

# Indicator
* **Positive Convexity iIndicator** :The average price implies the cost of chips at a certain time (the weighted volume average seems to be easily blunted and not as sensitive as the EMA), the first order derivative of the EMA represents the convexity of the average cost at different time periods, and the second order derivative is the positive or negative of the convexity

平均价格意味着一定时间内的筹码成本（加权成交量平均数似乎容易钝化，不如EMA敏感），EMA的一阶导数代表不同时间段的平均成本的凸性，二阶导数是凸性的正负值。

快慢线使用21，55，144，该指标并不直接给出多空信号，而是通过对比不同时间下的凸性程度，正负性作为辅助指标，参考多空趋势的可持续性。

![image](https://github.com/alniente/Tradingview_Indicators/blob/main/snapshot_preview_EMAconvexity.png)
```
//@version=4
study("convexity")

slope21=log(ema(close,21)/ema(close,21)[1])
slope55=log(ema(close,55)/ema(close,55)[1])
slope144=log(ema(close,144)/ema(close,144)[1])

plot(0,"0",color=color.black)
plot(slope21,"21slope",color=color.red)
plot(slope55,"55slope",color=color.blue)
plot(slope144,"144slope",color=color.purple)

```
```
//@version=4
study("minus/plus")

slope21=log(ema(close,21)/ema(close,21)[1])
slope55=log(ema(close,55)/ema(close,55)[1])
slope144=log(ema(close,144)/ema(close,144)[1])

convexity(close, length) => log(ema(close, length)/ema(close, length)[1])

Dconvexity21 = log(convexity(close,21)/convexity(close,21)[1])
Dconvexity55 = log(convexity(close,55)/convexity(close,55)[1])

plot(0,"0",color=color.black)
plot(Dconvexity21,"Dconvexity21",color=color.red)
plot(Dconvexity55,"Dconvexity55",color=color.blue)

```
