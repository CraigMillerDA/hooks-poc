# Proof of Concept Hooks for Uniswap V4

The following hooks were created as part of the Uniswap Foundation Grant. The purpose of the Grant was to showcase the new UniswapV4 Hooks feature and provide early feedback to the Uniswap Labs team.

## Liquidity Locking Hook (LLH)

The Liquidity Locking Hook locks the liquidity into the pool for a specified amount of time.

1. In order to compensate the liquidity providers for locking their liquidity, the hook will mint and distribute rewards among the liquidity providers.
2. The more liquidity is provided the more reward token the liquidity provider is entitled to.
3. The longer time the liquidity is locked the more reward token the liquidity provider is entitled to.
4. If the liquidity provider would like to withdraw liquidity before the locking period expires, he will suffer a penalty.
5. The early withdrawl penalty is distributed evenly amongst the rest of the liquidity providers.

## Liquidity Management Hook (LMH)

The Liquidity Management Hook will manage UniswapV4 ranges on behalf of the liquidity providers.

1. The liquidity provided to the hook is automatically split up into 2 ranges: the narrow and the wide range.
2. X% of the liquidity will be invested into the wide range which is currently the full Uniswap range.
3. 100-X% of the liquidity will be invested into the narrow range around the current price.
4. When the price moves as a result of a swap, the narrow range will automatically rebalance and follow the current price. This is done without involving any offchain component.

## Dynamic Fee Hook (DFH)

The Dynamic Fee Hook automatically changes the swap fee based on the pool's volatility. During higher volatility periods, higher fees are charged.

1. Volume is used as a proxy for price volatility.
2. All swaps on the pool increases the aggregated volume.
3. As time goes on, the aggregated volume automatically decreases.
4. The swap fee is a function of the aggregated volume at the time of the swap.

## Combo Hook

Hook that combines the functionaility of the Liquidity Locking Hook and the Dynamic Fee Hook.

## Request for Additional Hook Info

The following is an addition to the work by "BrokkrFinance". the Whitepaper/Readme was forked to do nothing other than to improve the Uniswap web3 app.

## Processes Needing More Explanation

Will users be able to utilize both, LLH and LMH simultaneously?

Can users individually set the LMH parameters? Will Uniswap provide different ranges for LMH? When a liquidity provider opts to use LMH, will ranges be set autonomously based on the amount of liquidity, volume and price volitility or possibly by another metric (such as Bollinger Bands)?

Uniswap v3 liquidity providers have to choose a fee in which to provide liquidity (ie. 0.3%, 0.1%, 0.05% and 0.01% fees). In Uniswap v4, do you expect that DFH will help with fragmentation of liquidity by keeping liquidity providers within the same pool?

Will DFH offset Impermanent Loss (IL) by increased fees during higher price volitility? What are the pros and cons for having 1 liquidity pool per pair of assets using DFH?

Are there any current developments, either theough this grant or any other grant that could allow liquidity (and swaps) to become chain-agnostic?
