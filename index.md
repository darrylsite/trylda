## Trylda - Advanced Binance trading bot

Trylda is a complete cryptocurrency trading bot. it currently works only for the Binance exchange, both for the Spot and the Future market.

You can have a quick presentation of the trading bot at [https://www.youtube.com/watch?v=_jbbHNzqvLs](https://www.youtube.com/watch?v=_jbbHNzqvLs)
[![trylda presentation](https://i9.ytimg.com/vi/_jbbHNzqvLs/mq2.jpg?sqp=CIjz3pQG&rs=AOn4CLDX19blwBTpvPcZ00Ti6sJlNtfuBw)](https://www.youtube.com/watch?v=_jbbHNzqvLs)

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

## Technicalrequirement
The bot is built using Java. The minimum requirement to run the software is Java 11.
The compilation of the project should be done in Java 17.
Because of Binance limitation on the APIs, 4 instances of the bot can be run per IP address.
