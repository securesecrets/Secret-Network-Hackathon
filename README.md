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

The router is where trades are executed by the users: https://github.com/securesecrets/shadeswap/tree/main/contracts/router
Pools on ShadeSwap are only in pairs -- for example, stATOM/stOSMO, meaning only the tokens in that pool can be traded. However, trades can be routed between pools. For example, if there is an stATOM/stOSMO pool, and an stATOM/ATOM pool, then a user would be able to trade their stOSMO for ATOM by first swapping stOSMO for stATOM, then stATOM for ATOM. The router contract allows such trades to happen in a single transaction.

The factory is where pools are created: https://github.com/securesecrets/shadeswap/tree/main/contracts/factory
Creation of pools is permissioned. However, you could launch the contracts yourself and play with the creation of your own pools if you like. The most useful thing in the factory is the ListAMMPairs query and GetAMMPairAddress if you are looking for the list of pools that are currently available.

The AMM pair contract is the heart of ShadeSwap: https://github.com/securesecrets/shadeswap/tree/main/contracts/amm_pair
These contracts are the actual pools of funds that trades are executed on. If you are trying to conduct arbitrage, these are the contracts you want to use. Refer to the README in the amm_pair repo for more information.

ShadeSwap LP contracts:

```
Constant Product:
 
 
 
SHD / stkd-SCRT
secret1qyt4l47yq3x43ezle4nwlh5q0sn6f9sesat7ap
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SHD / stATOM
secret1wn9tdlvut2nz0cpv28qtv74pqx20p847j8gx3w
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SHD / JKL
secret1uekg0c2qenz4mxwpg5j4s439rqu25p4a6wlhk6
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SHD / BLD
secret19964kxsa07lvz7pmujehpe6mrjfqxf73m86d3j
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
stATOM / stOSMO
secret1y5ay9sw43rqydyyds6tuam0ugt4rxxu3cmpc79
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SILK / stATOM
secret14xsrnkfv5r5qh7m3csps72z9vg49tkgf7an0d5
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SILK / stkdSCRT
secret1a6efnz9y702pctmnzejzkjdyq0m62jypwsfk92
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SILK / SHD
secret1l34fyc9g23fnlk896693nw57phevnyha7pt6gj
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SHD / SIENNA
secret1fe22vmduz3xt53r5vxcmd567z08g3yryzck8az
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
Stable Pairs:
 
 
 
SILK / IST
secret1lrlfevkpmwc0kfxl9e59x0er5d8pzh48t68m0e
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SILK / CMST
secret1cqk6t9jjzqelwm0f72n5u2utvljdfgsq047cqu
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SILK / USDC
secret1qz57pea4k3ndmjpy6tdjcuq4tzrvjn0aphca0k
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
SILK / USDT
secret10szrjlyza5u7yqcqvqenf28nmhwph4pad9csyw
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
Derivative Stable Curves:
 
 
 
ATOM / stATOM
secret1a65a9xgqrlsgdszqjtxhz069pgsh8h4a83hwt0
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
OSMO / stOSMO
secret1gxqsuht45uh2tpqdpru6z6tsw3uyll6md7mzka
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
JUNO / stJUNO
secret12wxpcquw2jx6an6da5nxyz6l7qd955u23ljcjn
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
sSCRT / stkdSCRT
secret1y6w45fwg9ln9pxd6qys8ltjlntu9xa4f2de7sp
e88165353d5d7e7847f2c84134c3f7871b2eee684ffac9fcf8d99a4da39dc2f2
 
```
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

The detailed list of messages are as follows:

```

/**
* message to deposit secret in exchange for stkd-SCRT
*/
const msgStake = (amount: string) => ({
msg: { stake: {} },
transferAmount: {
amount,
denom: 'uscrt',
},
});


/**
* message to unbond SCRT from stkd-SCRT
*/
const msgUnbond = (amount:string) => ({
unbond: {
redeem_amount: amount,
},
});


/**
* gets the staking contract info
*/
const msgStakingInfo = () => {
const time = Math.round(new Date().getTime() / 1000);
return { staking_info: { time } };
};


/**
* gets the user unbondings
*/
const msgUnbondings = (userAddress: string, viewingKey: string) => ({
unbonding: { address: userAddress, key: viewingKey },
});


/**
* gets the fees for staking/unbonding
*/
const msgFees = () => ({ fee_info: {} });

```
An Example way for secret.js to execute contract class

```

function msgExecuteContract({
sourceAddress,
contractAddress,
contractCodeHash,
transferAmounts,
msg,
}: {
sourceAddress: string,
contractAddress: string,
contractCodeHash: string | undefined,
transferAmounts?: Coin[],
msg: any,
}) {
return new MsgExecuteContract({
sender: sourceAddress,
contract_address: contractAddress,
code_hash: contractCodeHash,
sent_funds: transferAmounts,
msg,
});
}

```

Message Builders the class and definations.

```

* msg to deposit SCRT into the stkdScrt contract to receive stkdScrt
*/
function createMsgStkdScrtStake({
sourceAddress,
stkdScrtContractAddress,
stkdScrtCodeHash,
amount,
}: {
sourceAddress: string,
stkdScrtContractAddress: string,
stkdScrtCodeHash?: string,
amount: string,
}) {
const { msg, transferAmount } = msgStake(amount);


return msgExecuteContract({
sourceAddress,
contractAddress: stkdScrtContractAddress,
contractCodeHash: stkdScrtCodeHash,
transferAmounts: transferAmount !== undefined ? [transferAmount] : undefined,
msg,
});
}


/**
* msg to deposit stkdScrt to unbond scrt
*/
function createMsgStkdScrtUnbond({
sourceAddress,
stkdScrtContractAddress,
stkdScrtCodeHash,
amount,
}: {
sourceAddress: string,
stkdScrtContractAddress: string,
stkdScrtCodeHash?: string,
amount: string,
}) {
const msg = msgUnbond(amount);


return msgExecuteContract({
sourceAddress,
contractAddress: stkdScrtContractAddress,
contractCodeHash: stkdScrtCodeHash,
msg,
});
}


/**
* generalized msg to claim something from a contract
*/
function createMsgClaim({
sourceAddress,
contractAddress,
contractHash,
}: {
sourceAddress: string,
contractAddress: string,
contractHash?: string,
}) {
const msg = msgClaim(randomPadding());
return msgExecuteContract({
sourceAddress,
contractAddress,
contractCodeHash: contractHash,
msg,
});
}

```

Parsers for the query responses so that you can see the response interfaces.

```

* parses the response for the stkd-scrt contract info
*/
function parseStakingDerivativesInfo(data: StakingDerivativesInfoResponse): StakingDerivativesInfo {
const {
staking_info: stakingInfo,
} = data;
const {
price: exchangeRate,
rewards: communityRewards,
total_derivative_token_supply: supply,
unbond_amount_of_next_batch: nextUnboundAmount,
next_unbonding_batch_time: nextUnbondingBatchEstimatedTime,
validators,
} = stakingInfo;


return {
validators,
supply: convertCoinFromUDenom(supply, 6).toNumber(),
exchangeRate: convertCoinFromUDenom(exchangeRate, 6).toNumber(),
communityRewards: convertCoinFromUDenom(communityRewards, 6).toNumber(),
nextUnboundAmount: convertCoinFromUDenom(nextUnboundAmount, 6).toNumber(),
nextUnbondingBatchEstimatedTime: convertSecondsToMilliseconds(nextUnbondingBatchEstimatedTime),
};
}


/**
* parses the response for the stkd-scrt user unbondings
*/
function parseStakingDerivativesUserUnbondings(
data: StakingDerivativesUserUnbondingsResponse,
): StakingDerivativesUserUnbondings {
const {
unbonding: {
unbond_amount_in_next_batch: unbondAmountInNextBatch,
unbondings,
},
} = data;
return {
unbondAmountInNextBatch: convertCoinFromUDenom(
unbondAmountInNextBatch,
6,
).toNumber(),
unbondings: unbondings.map(({ unbonds_at: unbondsAt, amount }) => ({
unbondsAt: convertSecondsToMilliseconds(unbondsAt),
amount: convertCoinFromUDenom(amount, 6).toNumber(),
})),
};
}


/**
* parses the response for the stkd-scrt fees
*/
function parseStakingDerivativesFees(data: StakingDerivativesFeesResponse): StakingDerivativesFee {
const {
fee_info: feeInfo,
} = data;


const {
deposit: depositFee,
withdraw: withdrawFee,
} = feeInfo;
return {
depositFee: Number(depositFee) / 100000,
withdrawFee: Number(withdrawFee) / 100000,
};
}

```

### Shade Lend and SILK

Shade Lend is now live on mainnet.

### Liquidations:

A liquidation bot for shade lend simply queries the Vault Registry contract, which contains a list of all the available vaults on Lend. This is a paginated request:

`Vaults { starting_page: Uint128 }`

which returns a VaultsResponse:

```
pub struct VaultsResponse {
    pub vaults: Vec<VaultResponse>,
    pub page: Uint128,
    pub total_pages: Uint128,
    pub total_vaults: Uint128,
}
```

You can use a `starting_page` of `1` for your first query, and check if there are more pages in the `total_pages` value in the response. If there are more pages, you can make another query for the other pages and aggregate your results.

Then, you can individually query each vault for the list of risky positions:

`LiquidatablePositions { vault_id: Uint128 }`

Which returns a LiquidatePositionsResponse:

```
pub struct LiquidatablePositionsResponse {
    pub positions: Vec<PositionInfo>,
    pub vault_id: Uint128,
}
```

A `PositionInfo` has the following structure:

```
pub struct PositionInfo {
    pub vault_id: Uint128,
    pub position_id: Uint128,
    pub debt_amount: Uint256, // Will be zero for privacy reasons
    pub collateral_amount: Uint256, // Will be zero for privacy reasons
    pub ltv: Option<Decimal256>,
}
```


If there are risky positions, this response will contain the list of risky positions in that vault:

``

You may then execute the `liquidate` message on the contract for that vault, which will take SILK from the Stability Pool automatically, liquidate the position, and distribute the rewards. The wallet you used to execute the `liquidate` message will receive a reward in the form of 10% of the profits from the liquidation. For example, if $10,000 of debt was liquidated with stkd-SCRT at a 10% discount and stkd-SCRT was $1, then a liquidation would force the Stability Pool to purchase $10,000 worth of stkd-SCRT at a value of $0.90, resulting in 11,111 nominal stkd-SCRT of liquidation rewards. Since the real current value of stkd-SCRT is $1 in this example, 1,111 stkd-SCRT represents the profits. You as the operator of the liquidation bot would receive 10% of this -- or 111.1 stkd-SCRT. All you have to pay is SCRT gas to execute the liquidation, but if you're not the first one to liquidate the position, then you won't receive the reward.

The `liquidate` message has the following structure:

```
Liquidate {
    vault_id: Uint128,
    position_id: Uint128,
}
```

These messages are on the Vault Registry contracts here:

Minting Closed vaults (still liquidatable): 
```
address: secret18y86hldtdp9ndj0jekcch49kwr0gwy7upe3ffw 
code hash: 148a525ec7bffedfc41cbc5339bf22d9e310d49b65831a269c86774fb732948c
```  

Current vaults: 
```
address: secret1qxk2scacpgj2mmm0af60674afl9e6qneg7yuny 
code hash: ac5d501827d9a337a618ca493fcbf1323b20771378774a6bf466cb66361bf021
```

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
