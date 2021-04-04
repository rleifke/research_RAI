## RAI

Executive Summary

Built on Ethereum, RAI is a low volatility reflex index with minimal governance for decentralized financial applications to use. 
Utilizing an on-chain proportional-integral-derivative controller, the protocol is designed to react to various market pressures to maintain a stable market price that is within a small margin of what the system targets known as the redemption price. Unlike other algorithmic stablecoins that are also governance minimized, RAI allows for its exchange rate to float on secondary markets. Thereby, allowing for a unique mechanism design with negative interest rates. Similarly to MakerDAO, for which the reflexer system is a fork of, RAI is issued as an overcollateralized reflex index product, with its single collateral type being Ether. This is done by design to reduce external dependencies that could potentially translate to governance risks.

# Team
Reflexer Labs

Ameen Soleimani is the co-founder of SpankChain; an Ethereum based micropayment processor and held engineering roles at ConsenSys and NASA. He received an undergraduate degree in Chemical Engineering from Rensselaer Polytechnic Institute. 

Stefan Ionescu worked previously in research and development at Binance X and has held various software development roles at blockchain and fintech startups such as Cadence. 

# Overview 

There is no denying that stablecoins are foundational to a robust digital economy. But to fully appreciate reflexer’s mission, one must understand that pegged stablecoins are inherently flawed as a stable asset to build on in a trustless economy. Reducing external dependencies is essential as the applications that will be built on top of RAI can expect less operational risks as opposed to one that is highly centralized. Almost all of the stablecoins popular today such as USDC are centralized in some way; either by being pegged to the US dollar or even further, issued by a central authority with complete custodial control. The recently proposed STABLE ACT which would require stablecoin issuers to get the proper licenses is an example of the regulatory risk that comes with centralized stablecoin issuers . Moreover, these risks bleed into the synthetic and secondary assets for which the stablecoins are used as collateral. While the strengths and demerits of stability indirectly or directly backed by a central government can be argued, there is certainly a market and necessity for one that boasts minimal to near absence of direct governance. 

Chart.jpg

As shown in the chart above, RAI differs greatly from the current array of stablecoins. In part, that's because it's not, but rather a reflex index. The difference being that a reflex index is not pegged to a fixed exchange rate. Regardless, it still resides in the spectrum of traditional stablecoins in both its intention and potential use cases with an enormous addressable market.  


According to query data created by @hagaetc from Dune Analytics, stablecoin supply along with users has exponentially increased over the last two years.    As more applications are being built by minute, those numbers should only grow further and the demand for a capital efficient, governance minimized, and price stable cryptoasset will grow only greater.

Uniquely though, its mechanism while algorithmic is neither a rebasing model or a seigniorage shares system with multiple tokens. The reflex index uses an on-chain PID controller used as the primary stability mechanism. It is important to note that the redemption price is not the exchange rate, but merely a target price for the PID controller to adjust too. The goal is to get the market price as close to redemption price. 
On-chain autonomous PID controller

A controller is a feedback loop that “continuously calculates the control signal using the difference between the desired system state and the observed state” (Gauntlet). This is useful for algorithmically adjusting inputs to optimize for a desired output. Being one of the most popular and widely used feedback control mechanisms, a proportional-integral-derivatives (PID) controller has a great application in decentralized finance for creating price-stable assets. Having recognized this, Reflexer Labs have built an autonomous PID controller to dampen the volatility of Ether. There are three main components of a PID controller shown in the table below.


In the case of the reflex index, the steady state error is just the redemption
rate which is the difference between the market price and the redemption price. Ideally, the controller eliminates this difference all together so that the market price matches the redemption price so that there is no steady state error.

The redemption rate has the very direct effect of calibrating the redemption price around an arbitrary number, rand. Effectively, adjusting the redemption price of RAI accordingly to the ongoing market pressures during what is formally called the revaluing process. So if the market price is greater than the redemption price, the redemption rate is negative. In contrast, if the redemption price is greater than the market price, the redemption rate will be positive. 


# Trustless Leverage

Leverage is the name of the game. The reflexer system is almost entirely driven by the borrowing power of SAFE users. Essentially, RAI is minted when a SAFE user takes on debt. Therefore, when SAFE users have sufficient borrowing power; meaning they are well above the collateral ratio, and the redemption rate is negative, then the SAFE user will mint more RAI and sell them on the secondary markets. Another subtle factor influencing RAI’s money supply is the exchange rate of Ether. Any price appreciation in ETH has the effect of increasing the borrowing power of SAFE users as the value of their collateral is worth more relative to their collateral ratio. Thus, SAFE users can and are incentivized to mint more RAI. This is done by design, as each expansion of the money supply causes the market prices f0r RAI to decline.

Determining the borrowing power of a SAFE user is based on the current market price of Ether divided by the market price of RAI divided by the liquidation ratio.

borrowingPower = ETH/RAI/1.45 

Based on the redemption price at $3 and liquidation ratio at 145%, the borrowing power of Ether is a linear relationship with its price as expected. It decreases with a decrease in the price of Ether. At $1500 ETH, borrowing power is approximately $344 USD.


In later stages, reflexer hopes to introduce an autonomous rate setter that allows for adjustable (annual) borrowing rates which are currently fixed at 2% Once a SAFE is opened by a user, it continuously accrues debt based on the borrowing rate. This needs to be paid off in order for the user to withdraw from their collateral. An autonomous rate setter would lower the borrowing rate when the market price is higher than the redemption price. Incentivizing a SAFE user even more when the redemption rate is positive.  

# Liquidation 

As expressed above, each SAFE is overcollateralized at 145% which needs to be maintained to avoid risk of liquidation. Much like MakerDAO, there is a liquidation mechanism where if the safe falls under the collateral requirement, the protocol will sell the existing collateral as a safety blanket to keep the protocol solvent. Only keepers get to participate in the discounted Ether offering. At the moment there are 848 active safes representing 171,307 Ether locked up only 1 week after launching.  

Usually SAFEs with insignificant collateral categorized by the system as risk as opposed to safe will be more likely to get liquidated. This is a risk that SAFE users must be aware of before creating a SAFE. However, reflexer fiance currently allows for SAFE users to buy insurance on the Cover Protocol that would provide more collateral in SAFE, saving it from liquidation



At the movement there about $598,974 of total covered locked up. 

One of the ways the protocol protects itself from a detrimental liquidation event is by transferring risk to its protocol’s token holders who decide to participate in staking. If there is a liquidity crunch, stakers will be slashed and their tokens will be auctioned off to recapitalize the system. In exchange for taking on this risk, token holders will receive surplus created when RAI is minted and more protocol tokens. 

In the event of protocol failure that risks liquidity, a Global Settlement will be triggered. This refers to their “lender of last resort” mechanism intended to guarantee the net value of the underlying collateral to all RAI holders. This means that the RAI is redeemed at exactly its redemption price. Although global settlement is presumed to be triggered by burning of tokens, the system has also the capability of triggering settlement if one of these happen; Severe Price Feed Delays, System Migration, or Consistent Market Price Deviation. 

Once triggered, no SAFEs can be created, and the collateral price feeds as well as the redemption price will be frozen. Then in step 2, all outstanding assets are auctioned after which all RAI holders can lay claim to the underlying collateral based on the last recorded redemption price. 

# Governance Minimization Guide

Overtime, the system is designed to run fully autonomously without any direct interference. This will occur though a multi-stage process leaving many of the core contracts as is once deployed. There are certain requirements however that the GEB must meet before its governance is completely minimized. 


Note. https://docs.reflexer.finance/


STAGE 1:

Set 14 months after launch, the following smart contracts will be locked;



STAGE 2: 

Set 18 months after launch, the following smart contracts will be locked;



In this stage, the stabilityFeeTreasury will be locked. This contract is essential as it is responsible for paying all the costs associated with protocol operational expenses. Most importantly, allocating from the surplus to pay for the oracle network medianizer. It is a smart contract nearly identical to MakerDao that aggregates oracle feeds from a continuously updated list of approved oracles as well as paying for them. Currently, the runway is expected to be 6 months treasury surplus at roughly 5659 RAI.


STAGE 3:



While the majority of core contracts will not be upgradeable once deployed, for the few parameters that can be modified their implementation will be delayed by the Restricted Governance Module. Since the system is designed to be fully autonomous, reflexer has created a smart contract fittingly called Ice Age to impose deadlines for the gradual locking of the protocol from human intervention. That said, there is a fixed number of times that the contact deadlines can be delayed in order to fix critical bugs before the system becomes fully autonomous. 

Interestingly enough; even after full autonomy is reached, new reflex indexes can be deployed via the GEB framework. As of right now, the plan is to hold only one collateral type, but the GEB allows governance to create new ones in the future. In order to prioritize governance minimization, the collateral type must remain singular. Adding more collateral types as is the chase with multi-collateral MakerDao adds counterparty risks. 


# Conclusion

Despite early hiccups as expected, the PID controller has worked remarkably well and the floating exchange rate of the index has stayed consistently within a reasonable margin of the redemption price.


According to transaction data taken from Etherscan, the launch also attracted a healthy number of transaction through the protocol. 


A fork of Maker, RAI’s value proposition as a governance minimized reserve asset is an appealing one for asset managers and protocols who want to hold a portion of their funds in an uncorrelated and stable cryptocurrency. Synthetics for example are in dire need of low volatile asset exposure. Having a stable asset as collateral would give more time to exit positions. Even more exciting, redemption rates can go negative (currently at -67%). As a result, borrowing assets can effectively earn yield for the borrower. Never before has this been possible, thus creating a new frontier of financial applications namely for money markets and yield aggregators. 

There are trade offs for a governance minimized design however. For one, the reflexer protocol cannot influence the money supply directly without conducting open market operations. This leaves an immense amount of pressure on (rational) behavioral assumptions of SAFE users. Moreover, if demand for RAI is unsupported, there arises substianal risk for continuous devaluation because RAI can only be generated by SAFE users. Moreover, the protocol benefits, and to a degree depends on Ether’s long term price trajectory. In the hypothetical case Ether goes to zero, so will the reflex index. Finally, RAI’s scalability is limited by users borrowing power from its SAFE. Like many protocols that are overcollateralized to be trustless, they are capital inefficient to their 1:1 pegged stablecoin counterparts. 

That said, Ether has become the de-facto reserve asset for the entirety of the DeFi space. Even if chain interoperability continues to improve, there isn't much reason to expect this to change anytime soon. For now, the near monopoly Ethereum has over developer activity is protecting Ether’s value and thereby RAI. In market size, with 46,868,302 RAI circulating in comparison to other stablecoin competitors like USDC with billions in circulation, RAI certainly has substantial room to grow. 







# Key Takeaways

Built to have low volatility and minimal governance.
Uncorrelated reserve asset for DeFi
Utilizes negative interest rates 
Redemption rate revalues the redemption price continuously
SAFE users mint RAI when they generate debt
Borrowing power is critical to the system 

# References 

https://www.mechanism.capital/algorithmic-stablecoins/
https://medium.com/gauntlet-networks/feedback-control-as-a-new-primitive-for-defi-27b493f25b1
https://ctms.engin.umich.edu/CTMS/index.php?example=MotorPosition&section=ControlPID

Key Terms

Redemption price:
The target price the reflex index attempts to stabilize around. 


Redemption rate:
Revalues the redemption price of RAI with the difference between market price and the redemption price.


Borrowing Rate
Interest accrued on SAFEs immediately after opening.


