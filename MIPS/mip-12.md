---
mip: 12
title: Add Alchemix alUSD/mUSD Feeder Pool
status: Proposed
author: shubidoobi, Dimitri Golecko (@dimsome), Nick Addison (@naddison36)
discussions-to: https://forum.mstable.org/t/discussion-alchemix-alusd-musd-fpool/497
created: 2021-06-1
---

## Simple Summary

It is proposed to add a Feeder Pool as specified in [MIP 9](./mip-9) for [Alchemix](https://alchemix.fi/) alUSD/mUSD. Alchemix alUSD is a stablecoin backed by yield that is generated by the Alchemix Protocol. This addition would provide interesting arbitrage opportunities with low impermanent loss risk while helping to keep alUSD close to peg, all the while earning swap fees and MTA for LPs who want exposure to both mUSD and alUSD.

## Abstract

Alchemix is a decentralized borrowing protocol that allows users to draw self-repaying loans in their native stablecoin alUSD against DAI as collateral. Users can deposit DAI and mint alUSD on Alchemix at a minimum collateral ratio (MCR) of 200%. This alUSD is a stable asset pegged to the price of USD. alUSD can be swapped for other stablecoins or assets or transmuted back at any time for DAI.

Adding alUSD as a Feeder Asset would enable users of Alchemix to directly either swap alUSD using the Feeder Pools to any other on mStable available stablecoins or deposit directly into SAVE. This addition would earn additional yield for the savers, for liquidity providers, increase TVL of mStable, foster new potential collaboration, and add value to MTA.

The mUSD from this proposed Feeder Pool will be handled according to [MIP 11](./mip-11), however the integration specified there will only be enabled upon sufficient liquidity.

## Motivation

This proposal seeks to overall increase mStable's composability with the ecosystem as well as to increase yield for liquidity providers and savers alike.

Alchemix, since its inception, has grown to a TVL at the time of writing of [\$1.48 Billion](https://defillama.com/protocol/alchemix), while [401 Million](https://etherscan.io/token/0xBC6DA0FE9aD5f3b0d58160288917AA56653660E9) alUSD are in circulation. Additionally, alUSD has already generated a fair share of swap volume on other protocols (~\$20 to 60 Million daily trading volume on [alUSD/TriPool](https://curve.fi/alusd)). This shows that there is already a healthy demand for swaps and that alUSD is well integrated and circulated in other DeFi products.

The unique feature of Alchemix alUSD is that there is no risk of liquidations, as the loan pays off itself. This reduces the risk of a depegging of this asset during volatile market swings substantially. Additionally, since alUSD is backed by DAI, the risk of alUSD losing value is relatively low.

This proposal also could be the first step in an ongoing collaboration with the Alchemix team to integrate more assets, and to participate in the overall extremely positive sentiment in the community around this new DeFi primitive.

## Specification

A new instance of the `FeederPool` contract will be deployed with the following parameters:

- Name: mUSD/alUSD Feeder Pool
- Symbol: fPmUSD/alUSD
- Amplitude coefficient (A): 100
- Swap fee: 0.04% (4 basis points)
- Redemption fee: 0.04% (4 basis points)
- Min bAsset weight limit: 3%
- Max bAsset weight limit: 97%
- alUSD integration: none as alUSD is not currently supported by Aave or Compound
- mUSD integration: none initially. Iron Bank integration can be added later when the pool has grown and there is borrowing of mUSD from Iron Bank.

The `alUSD` smart contract address is `0xBC6DA0FE9aD5f3b0d58160288917AA56653660E9`

The `mUSD` smart contract address is `0xe2f2a5c287993345a840db3b0845fbc70f5935a5`

A new instance of the `BoostedSavingsVault` contract will be deployed with the following parameters:

- Name: v-mUSD/alUSD fPool Vault
- Symbol: v-fPmUSD/alUSD

This MIP grants the ProtocolDAO permission to adjust the Amplitude coefficient (A) when deemed necessary and to integrate the Iron Bank as specified in [MIP 11](./mip-11).

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).