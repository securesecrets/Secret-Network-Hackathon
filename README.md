## Shade Protocol Hackathon Reference

This document is a reference for everything you will need to know about Shade Protocol to participate in the Secret Network hackathon.

If your question is not directly answered by this document, stop by our discord. We have a dedicated hackathon channel and we'll do our best to answer your questions.

Our discord is: https://discord.gg/shade-protocol-905665558610051113

### Shade Protocol Overview

Shade Protocol is an interconnected suite of DeFi primitives that provides a unified user experience for DeFi participants. 

Our full docs are available at: https://docs.shadeprotocol.io/shade-protocol/
Our whitepaper, if you're looking for even more in-depth information, is available at: https://shadeprotocol.io/wp-content/uploads/2023/01/Shade-Protocol-Whitepaper.pdf

### GitHub Links

Main Shade Repo: https://github.com/securesecrets/shade  
Shade Oracles: https://github.com/securesecrets/shade-oracle  
Better Secret Math, gas optimized math operations for Secret Network: https://github.com/securesecrets/better-secret-math  
ShadeSwap: https://github.com/securesecrets/shadeswap  

### ShadeSwap

ShadeSwap is our Decentralized Exchange (DEX). It features two types of pools, Constant Product Market Making (CPMM) pools and Concentrated Liquidity (CL) pools.

Our CL pools implement the Silk Swap curve, giving us control over the price range that trades are executed if the prices of the assets in the pool are predictable. The SilkSwap whitepaper is available at: https://blog.shadeprotocol.io/content/files/2022/11/SilkSwap--2-.pdf

The interfaces for our contracts is available in the ShadeSwap repo. In this document, we will summarize the system architecture.

The router is where trades are executed by the users: https://github.com/securesecrets/stableswap/tree/main/contracts/router
Pools on ShadeSwap are only in pairs -- for example, stATOM/stOSMO, meaning only the tokens in that pool can be traded. However, trades can be routed between pools. For example, if there is an stATOM/stOSMO pool, and an stATOM/ATOM pool, then a user would be able to trade their stOSMO for ATOM by first swapping stOSMO for stATOM, then stATOM for ATOM. The router contract allows such trades to happen in a single transaction.

The factory is where pools are created: https://github.com/securesecrets/stableswap/tree/main/contracts/factory
Creation of pools is permissioned. However, you could launch the contracts yourself and play with the creation of your own pools if you like. The most useful thing in the factory is the ListAMMPairs query and GetAMMPairAddress if you are looking for the list of pools that are currently available.

The AMM pair contract is the heart of ShadeSwap: https://github.com/securesecrets/stableswap/tree/main/contracts/amm_pair
These contracts are the actual pools of funds that trades are executed on. If you are trying to conduct arbitrage, these are the contracts you want to use. Refer to the README in the amm_pair repo for more information.

### Liquid Staked SCRT (stkd-SCRT)

Shade Protocol's staking derivative, stkd-SCRT, allows users to earn yield from staking SCRT while still having a liquid token that can be used in DeFi. We do not have public documentation on the contract interface, but here are the most useful messages that are available on the stkd-SCRT contract, other than the standard SNIP-20 messages.

```
    /// Stake SCRT
    Stake {},
    /// Unbond SCRT
    Unbond {
        /// amount of derivative tokens to redeem
        redeem_amount: Uint128,
    },
    /// claim all unbonded SCRT that has reached maturity
    Claim {},
```
This should be sufficient for arbitrage use cases, and any other programmatic use case such as building an interface that allows you to manage a stkd-SCRT position.

Here is the full list of available query messages on the stkd-SCRT contract:

```
pub enum QueryMsg {
    // staking
    /// display the validator addresses, amount of bonded SCRT, amount of available SCRT not
    /// reserved for mature unbondings, amount of pending staking rewards not yet claimed,
    /// the derivative token supply, and the price of the derivative token in SCRT to 6 decimals
    StakingInfo {
        /// time in seconds since 01/01/1970.
        time: u64,
    },
    /// display the address' amount of SCRT that is immediately claimable, the amount of SCRT
    /// that is unbonding, the derivative token balance, and the SCRT value of held derivative tokens
    Holdings {
        /// address whose holdings to query
        address: HumanAddr,
        /// the address' viewing key
        key: String,
        /// time in seconds since 01/01/1970.
        time: u64,
    },
    /// display list of unclaimed unbondings
    Unbonding {
        /// address whose unclaimed unbondings to display
        address: HumanAddr,
        /// the address' viewing key
        key: String,
        /// optional page number to display
        page: Option<u32>,
        /// optional page size
        page_size: Option<u32>,
        /// optional time in seconds since 01/01/1970.  If provided, response will
        /// include the amount of SCRT that can be withdrawn at that time
        time: Option<u64>,
    },
    /// display list of admin addresses
    Admins {},
    /// display the msg limits to an admin
    MsgLimits {
        /// admin address making the query
        address: HumanAddr,
        /// viewing key of this admin address
        key: String,
    },
    /// display the fee collector address and fee rate using 5 decimal places: i.e., 1000 = 0.01000 = 1%
    FeeInfo {},

    // snip 22
    TokenInfo {},
    ContractStatus {},
    Allowance {
        owner: HumanAddr,
        spender: HumanAddr,
        key: String,
    },
    Balance {
        address: HumanAddr,
        key: String,
    },
    TransferHistory {
        address: HumanAddr,
        key: String,
        page: Option<u32>,
        page_size: u32,
    },
    TransactionHistory {
        address: HumanAddr,
        key: String,
        page: Option<u32>,
        page_size: u32,
    },
    WithPermit {
        permit: Permit,
        query: QueryWithPermit,
    },
}
```

### Shade Lend and SILK

Shade Lend is about to launch on mainnet, so depending on when you're reading this, it might not be available yet. Lend is expected to live on April 19th. This document will be updated once the contracts are public.

## Sponsored Projects

Shade Protocol is sponsoring a number of projects with our own rewards, paid in SHD tokens. The projects are broken into two tiers -- Tier 2 projects are generally quite simple projects and are a good start if you're new to development, or you want to experiment with arbitrage trading, liquidations, and other off-chain MEV activities. Tier 1 projects are major projects tied to a significant grant. For the scope of the hackathon, MVPs will be accepted, but the full reward amount is contingent on an extended grant to fully integrate the product into the Shade Protocol application with proper testing, documentation, and auditing. These are best tackled by experienced developers or ambitious teams.

Rewards for sponsored projects are in addition to and separate from the existing Secret Network Hackathon prize pool, but if you choose to tackle one of our sponsored projects they are acceptable entries to the Hackathon as well. All functionality must be on mainnet to be eligible for rewards and must be open source. Many of the projects allow you to earn money passively just by running the bots, so you have additional incentive to build and maintain them even after the Hackathon is over. Doing so contributes to the decentralization of the protocol.

**We are providing up to 30,925 SHD of rewards. At a price of $7 per SHD, that's $216,475 of rewards on top of the Secret Network Hackathon prize pool!**

### Tier 2 Projects

- Build an arbitrage bot or smart contract that utilizes ShadeSwap's liquidity pools to execute staking derivative arbitrage using Stride's derivatives and IBC. You would purchase staking derivatives at a discount on ShadeSwap, transfer them from Secret Network to Stride using IBC, and trigger an unbond to capture the arbitrage. This project is simple and the skills you learn can be applied to any other staking derivative arbitrage opportunity on any other network. 
    Milestone 1: Build a bot that executes the arbitrage described above. +125 SHD
    Milestone 2: Build a bot that executes the arbitrage for all available staking derivatives on ShadeSwap, and also utilizes the ShadeSwap router to capture arbitrage on not-CL pools. +50 SHD

- Build an arbitrage bot or smart contract that utilizes ShadeSwap's liquidity pools to execute staking derivative arbitrage using Shade Protocol's stkd-SCRT. You would purchase staking derivatives at a discount on ShadeSwap and trigger an unbond on stkd-SCRT to capture the arbitrage. This project is even simpler because it does not require IBC. 
    Milestone 1: Build a bot that executes the arbitrage described above. +125 SHD

- Build a liquidation bot that executes liquidations on Shade Lend. Liquidations on Shade Lend are public -- anyone can call the function to execute a liquidation. It does not cost anything except SCRT gas to execute liquidations, and you receive 10% of the profits of all liquidations as a reward for liquidation risky positions and contributing to the security and decentralization of the protocol. 
    Milestone 1: Build a bot that executes liquidations on Shade Lend. +125 SHD
    Milestone 2: Make the bot sell the accrued liquidation rewards for SILK. +50 SHD

- Build an arbitrage bot or smart contract that executes arbitrage across ShadeSwap's stablecoin pools. SILK is present in all of our pools, and there are multiple dollar stablecoins available on ShadeSwap. This means there is arbitrage to be captured when the pools are not valuing SILK equally. An arbitrage bot would identify SILK price discrepancies and purchase SILK at a cheap price in one pool, and sell it for a greater price in another pool until the prices are equalized.
    Milestone 1: Build a bot or smart contract that executes the arbitrage described above. +125 SHD
    Milestone 2: Build a contract that allows users to deposit SILK, and if you haven't already, convert the arbitrage bot into a smart contract that executes the arbitrage on-chain using the SILK deposited in the other smart contract. Distribute profits to depositors, and ensure all arbitrage trades are profitable. +50 SHD
    Milestone 3: Build a front end for this application -- **this could be your own protocol!** +50 SHD

- Build an arbitrage bot or smart contract that executes arbitrage between ShadeSwap's stablecoin pools and higher liquidity ETH pools (e.g. Curve, Uniswap V3, etc). This involves a Secret Network contract, a solidity contract, IBC integration, and Axelar GMP integration. This is a more involved project if you're looking for a challenge, but this will be the most profitable arbitrage by a significant margin, and also the most valuable for the protocol.
    Milestone 1: Build a bot or smart contract that executes the arbitrage described above. +125 SHD
    Milestone 2: Build a contract that allows users to deposit SILK, and if you haven't already, convert the arbitrage bot into a smart contract that executes the arbitrage on-chain using the SILK deposited in the other smart contract. Distribute profits to depositors, and ensure all arbitrage trades are profitable. +50 SHD
    Milestone 3: Build a front end for this application -- **this could be your own protocol!** +50 SHD

### Tier 1 Projects

- Build a Yearn-style product that allows users to deposit SILK, and allows the creation of arbitrary strategies that can be plugged into the contract that utilize deposited funds to generate yield. This is the simplest Tier 1 project and involves the development of ERC-4626, ERC-5115, or other related token standards on Secret Network. Rewards must be compounded and distributed to depositors.
    Milestone 1: Build a POC that enables the behavior described above, along with two strategies utilizing deposited SILK, such as depositing funds into the Shade Protocol Earn pool, or providing liquidity on ShadeSwap. +350 SHD
    Milestone 2: Minimize risk to depositors by only building strategies with expected profitable outcomes, such as LPing in a stablecoin pool or Earn pool. Additionally, enable the creation of strategies that accept any input token, not just SILK. +150 SHD
    Milestone 3: Include two configurable fees: a performance fee that takes a percentage of all generated yield, and a management fee that takes a percentage of deposited principal funds. The fees should be denominated in Annual Percent Rates (APR). +150 SHD
    Milestone 4: Build a fully functional front end that allows users to interact with your contracts -- **this could be your own protocol!** +150 SHD
    Milestone 5: Productize your project into a fully functional MVP that meets our grant requirements. **+9,200 SHD!** Grant requirements will be listed here when available:

- Implement Trader Joe's Liquidity Book as a Secret Network contract that works with the ShadeSwap pool factory. Trader Joe Liquidity Book documentation is available here: https://docs.traderjoexyz.com/ and source code is available here under MIT license: https://github.com/traderjoe-xyz/joe-v2/. This is a protocol on Avalanche which is an EVM based blockchain, so you must be comfortable with Solidity to understand the source code but do not need to do any Solidity development.
    Milestone 1: Build a POC that allows you to launch a pool that implements the Liquidity Book spec, complete with a rudimentary front end that allows you to manage your LP position. +350 SHD
    Milestone 2: Implement a pool factory and router that allows you to manage the deployment of pools permissionlessly, as well as route trades through multiple pools. +150 SHD
    Milestone 3: Productize your project into a fully functional MVP that meets our grant requirements. **+19,500 SHD!** Grant requirements will be listed here when available:
