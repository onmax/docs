---
id: limit-orders
title: Range Orders
---
Customizable liquidity positions, along with single-sided asset provisioning, allow for a new style of swapping with automated market makers: the **range order**.

In typical order book markets, anyone can easily set a limit order: to buy or sell an asset at a specific pre-determined price, allowing the order to be filled at an indeterminate time in the future. 

With Uniswap V3, one can approximate a limit order by providing a single asset as liquidity within a specific range. Like traditional limit orders, range orders may be set with the expectation they will execute at some point in the future, with the destination asset available for withdrawal after the spot price has crossed the full range of the order. 

Unlike standard limit orders, where the order maker typically pays fees when the order is filled, the range order maker **generates fees** while the order is filled. This is due to the range order technically being a form of liquidity provisioning rather than a typical swap. 



## Possibilities of Range orders

The nature of AMM design makes some styles of limit orders possible, while others cannot be replicated. The following are four examples of range orders and their traditional counterparts; the first two are possible, the second two are not. 


### Profit Taking 


> The current price of a DAI / ETH pool is 1,500 DAI / ETH. You would like to sell your ETH for DAI when the price of ETH reaches 1,600 DAI / ETH. This is possible, as the price space above the spot price is denominated in ETH. You can provide ETH at a price of 1,600 DAI / ETH and have the order filled when the spot price crosses your position.

### Buying the Dip

> The Current price of a DAI / ETH pool is 1,500 DAI / ETH. You expect that ETH will rebound after it drops to 1,000 at the next market downturn, so you would like to place a range order swapping DAI to ETH at the price of 1,000 DAI / ETH. This is possible, as the price space below the spot price is denominated in the lower-priced asset. You can provide DAI at the price of 1,000 DAI / ETH, which will be swapped for ETH when the spot price of ETH drops past 1,000 DAI / ETH.


As the above examples show, In Uniswap V3, the two paired assets in a given pool are separated above and below the spot price, with the higher price asset available above the spot and the lower-priced asset below. 

The following examples show limit order styles that are unable to be replicated due to the separation of assets in price space.

### Above-market Limit Orders

> The current price of a DAI / ETH pool is 1,500 DAI / ETH. You expect the price of ETH, once it hits 2,000, will rocket up to 3,000. So you would like to place a range order from DAI to ETH at a price of 2,000 DAI/ETH. This is not possible as the price space above 1,500 DAI / ETH is denominated in ETH - and thus, you cannot provide the DAI necessary at your desired price to be swapped into ETH.

### Stop-loss Orders

> The current price of a DAI / ETH pool is 1,500 DAI / ETH. You expect once the price of ETH drops to below 1,000, it will tank to 200. So you would like to place a range order from ETH to DAI at a price of 1,000. This is not possible as the price space below the spot price is denominated in DAI, and so you cannot allocate the ETH necessary at 1,000 to be swapped into DAI. 

One important distinction: range orders, unlike traditional limit orders, will be **unfilled** if the spot price crosses the given range and then reverses to recross in the opposite direction before the destination asset is withdrawn. While you will be earning LP fees during this time, if the goal is to exit fully in the desired destination asset, you will need to keep an eye on the order and manually remove your liquidity when the order has been filled.

 
## Fees
 
Because fees are generated in both tokens when swapping, the fees due to your liquidity position will be denominated in both tokens of the given pair. In any of the above examples, after swapping ETH for DAI, or DAI for ETH, a small amount of both ETH and DAI will be due to your account as liquidity provisioning rewards.

Approaches to concentration when setting range orders are up to the user. Selecting a wider range may generate more fees if there is price churn within your range, at the cost of increasing the risk of having your order unfilled if the spot price reverses before completing your full range.