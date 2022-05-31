## Trylda - Advanced Binance trading bot

Trylda is a complete trading cryptocurrency trading bot. it works currently only for the Binance exchange both for the Spot and the Future market.

You can have a quick presentation of the trading bot at https://www.youtube.com/watch?v=_jbbHNzqvLs

The bot is built in Java so it can be deployed on any platform bot Linux and Windows. I started the project in January 2021.

## Features

The bot supports :
* Own scripting language for dynamic strategy
* All major technical indicators
* Ashi Heikin candles
* Multi timeframe
* Stop loss take profit
* Trailing orders
* Backtesting

### Example of a strategy using the Ashi Heikin candes & EMA

```
[Settings]
    let tradeAmount = input.getTradeAmount()

    let canGoLong = 0
    let canGoShort = 0


[Can go long]
    Strategy.useAshiHeikinBars(true)
    if indicator.getEma(8) < indicator.getEma(5)
    Strategy.setCandleIndex(-1)
    if indicator.getEma(8) > indicator.getEma(5)
      canGoLong = 1
      Strategy.useAshiHeikinBars(false)

[Go Long]
    Strategy.useAshiHeikinBars(false)

    let stopLoss = math.mult(currentMarketPrice(); 0.993)
    let diffStopLoss = util.diffPercent(currentMarketPrice(); stopLoss)

    Strategy.defineAsLongStrategy()
    if noPendingOrderExist()
    if canEnterPosition()
    if fundAvailable()
    if canGoLong == 1 && diffStopLoss > 0.3
    if currentPriceLowerThanCloseLong(2, 3600)
         let orderId = openLongPosition(tradeAmount)
         setStopLoss(orderId, stopLoss)

[Long - Exit position]
    Strategy.defineAsLongStrategy()
    if hasCryptoBalance()
    if marketPriceHigherThanAnyLongTrade()
    if currentPriceProfitable()
        exitLongPosition()
```
