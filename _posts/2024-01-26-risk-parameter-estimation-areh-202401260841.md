---
layout : post 
title  : An Overview of Lending Parameter Estimation for Crypto Markets
snip   : Risk Considerations for Crypto Protocols
---

# Introduction

Decentralized finance (DeFi) lending protocols like Ethereum Credit Guild and
Ajna have opened up the creation of new, cryptocurrency based lending markets
that cover a long-tail of tokenized assets. One under-discussed topic in the
DeFi space is the generation of lending terms and collateral selection as an
overall credit risk framework. This paper discusses a rough overview of the
problem for these DeFi credit markets establishing why it's important to new
participants operating in the DeFi credit space. A second section is included
that explains basic frameworks that should be used as a panel of risk
assessments when considering credit markets, which should be barebones risk
metrics for any new lending terms. Lastly, new avenues are discussed as
possible options for credit operators that have appropriate capital, that are
possibly under-explored opportunities in crypto-based credit markets. The
overall goal is to explore crypto-credit markets for beginners, and generate
interest in development in new products that can serve these markets.

I am also available to join risk engineering and analytics teams in developing
these products for protocol operators if interested. Feel free to reach out to
me.


# Problems in Crypto Lending

## Lending Volatile Assets 

A simplified model for lending when collateralized by volatile assets is that
the system should try to optimize:

    1. Selecting an interest rate to make lending profitable while accounting
       for possible default.
    2. Development of agreed upon liquidation terms where in the event of
       default, collateral can be quickly sold to recuperate debt.

While these may seem trivial, global lending rates are a competitive market
where participants may undercut other lenders to gain market share. Also,
volatile collateral may rapidly move against lenders where after liquidation
the debt may never be recuperated in full. The interest rate is in some sense
both insurance against default (risk premium) and a payment that charges a fee
for general credit (time premium). The difficulty in the cryptocurrency space
is compounded due to the extreme volatility on the upside and downside of both
collateral assets and lending dollars.

## Equity Risk Models 

An additional quirk in cryptocurrencies is that despite the name, not only do
cryptocurrencies as an asset class include assets that should not be considered
"currencies", many users within the space and outside of it cannot agree on
whether the assets are equities or commodities.

While traditional businesses can lean on governments to enforce equity
contracts and associated contractual cashflows, cryptocurrencies that use
blockchain technologies generally only encode fees as income as the base
"cashflow" for not only protocol applications, but blockchains themselves. From
that, there are analysts who treat these system's tokens as "equity" and model
valuations based on discounted cashflow. In standard equity models, pricing
cashflows under discount is seen as a sort of collateral that lenders use to
assess risk of loans and default probabilities, but it is unclear whether this
model works in the blockchain space.

Coupled with this, many cryptocurrencies serve a "commodity" use-case as they
price abstract refinement of data, computation, or capital allocation in the
future. Some analysts model systems asserting they are informational
commodities who's value is not dependent on cashflows but future refinement of
goods that have downstream profits for purchasers, which adds a complex
valuation dynamic in the supply chain of information processing and data
storage.

Many cryptocurrencies can be argued as both an equity premium that sells a
commodity, or a commodity itself that is used to refine other (financial)
products. These difficulties make the models of using traditional equity risk
frameworks suspect since these systems sit somewhere between cashflow
generating organizations, and simple information systems.


## Problems Unique to Ethereum/Blockchain

Most protocols enable auctions for collateral liquidatation if debt is deemed
bad and the system wishes to call back the loan. Problems occur in a
free-market system such as Ethereum during these auctions, since there is no
real obligation from participants to purchase the auctioned debt. If a lending
system like a bank wishes to liquidate collateral in traditional markets, there
is some contractual agreements between market-maker that they must operate and
quote reasonable prices, and some legal protections in place if this obligation
isn't met. In Ethereum and decentralized finance, this obligation isn't a
requirement, and in the face of large liquidations, market makers may not
re-purchase assets at a value that covers debt.

Another larger issue is meta-level effects of blockchain systems that may allow
the blockchain substrate itself to be "gamed", to allow for auction buyers to
purchase significantly discounted collateral during the auction by attacking
the substrate itself. While this is unlikely today, during previous large scale
crashes, Ethereum and other side-chains were "spammed" by nefarious actors,
preventing other auctioners to bid for liquidated collateral. Modern collateral
auctions today have risk mitigation techniques to help prevent this type of
attack, but this risk is present and may affect credit pricing as a risk
premium lenders must cover.

# Recommendations

## VAR/Volatility Metrics

A standard metric for lending rates is to take account of the daily standard
deviation of percent returns, i.e. volatility. Under statistical normality
assumptions, this works out to be a tractible metric to discuss and rank risk.
Problems do arise as this method smooths outliers, which leads to Value At Risk
(VAR) metrics as a more robust non-parametric statistic. Here, one ranks losses
across a sample range and period, and can describe "top 2%" or "top 5%" losses.
This method is more robust and can take into consideration of outliers without
the smoothing effect typical in statistical metrics.

One consideration for cryptocurrencies unfortunately is both VAR and volatility
metrics have some of the highest percent changes in assets. Under normal
assumptions, yearly volatility of cryptocurrency ranges between 50 and 90%. It
is difficult to generate a real discussion of lending VAR/Volatility metrics
across cryptocurrencies when volatility is so high.

While these metrics in general difficult to work with in lending
parametrization, they should likely be used as part of a cohort of lending
factors. Also, lending operators should use these metrics as a way to identify
ranks of collaterals to understand comparative risks between assets.
Unfortunately in downturns of markets, many crypto based assets correllate
together and down, so comparative metrics should be taken with skepticism. 

## Modified Merton Model 

Using the Merton Model derived from the Black-Scholes equations, one can
produce a closed form estimate of default probability for a particular lending
agreement. This model utilizes:

    - Loan To Value = Debt Value / Collateral Value (LTV)
    - Expected Collateral Return Rate
    - Collateral Volatility

While the specifics number of the risk-free rate and collateral volatility can
be debated, since they do not reflect respectively the collateral's growth rate
and parametric volatility is an estimate respectively, this particular model
can serve as a way to guage a particular lending agreement's margin of safety
as terms are created. As well, this particular model's tractibility allows for
real time monitoring of lending parameters.

For real time monitoring, one could generate a ruleset that identifies key
metrics and calls the loan if metric limits are hit. In particular, metrics
that should trigger loan recalls should include:

    - An increase in default probability to a specific level holding volatility
      fixed as collateral value drops.
    - An increase in default probability when short-time frame volatility is
      substituted with yearly volatility. 
    - A change in default probability when substituting collateral's expected
      growth rate with compared to the Risk-Free Rate. 

The benefits of this particular model is one can compare these probabilities in
a tractible way. Rulesets defined by changes in probability make discussions
and changes of lending parameters measurable leaving little room for
interpretation. Lending protocols should have some method of default
probability included, and can make adjustment based on the Merton Risk model as
a starting point. More robust estimation could include substituting the
collateral volatility with VAR which measures worst case losses, or taking half
of the short term risk free rate as a return parameter.

## Tranched Lending Markets

Novel developments in the auction and recapitalization of bad loans are
on-going in the crypto lending market space. Newer protocols have attempted
continuous loans where collateral is auctioned off in real time to reflect
price changes, effectively fixing a loan to value. These protocols engage in
various flavors between continuous and partitioned auctions, but this model
effectively is the generation of "risk tranches". In traditional finance, risk
tranches have lots of historic precidence where a user's assets may be
contractually sold off in chunks if price targest are hit, but a closed form
model is just to take partitions of the users assets, and assert specific LTV
requirements for each tranche.

While tranched lending isn't particularly complex, one could imagine for a
system with a new type of collateral and a target lending cap, to partition the
cap into "chunks" with ranked LTV, where higher LTV commands higher payment
rates. As capacity is reached on lower LTV (with cheaper rates), it is assumed
the market would reach an equilibrium where most of the capacity with higher
LTV is un-utilized. This particular system of course requires maintenance of
lending rates and creation of new buckets as some risk tranches may be
auctioned under high collateral stress, but serves to help protect lenders from
a shock and major loss in a single lending agreement.

# Other Considerations

## AI/ML 

Since the cryptocurrency world has access and information to individual
accounts, scoring debtors with credit risk metrics is possible. Some factors
could include account volume traded, account age, maximum net worth, and other
metrics that can help understand the risk profile of the lending agreement
while taking into consideration the specific debtor. This could also be coupled
with automated machine learning systems to develop account-specific lending
agreements. While the decentralized finance space has yet to explore this area,
traditional finance's use of machine learning in credit risk models, taking
into account variables is not new and regularly used. It may be prudent for
mature lending markets to develop an in house quantitative risk team to profile
user accounts. Cost-permitting, development of AI/ML tools to generate
automated risk models using user-based features would be an entirely new
product class, but could be worth the investment to help reduce losses for
cryptocurrency based lending protocols, and possibly be a revenue generating
product for other market participants.

## Liquidity

Liquidity models of specific DeFi markets are not yet mature and mainstream. In
particular, liquidity is linked to volatility and VAR since available liquidity
soaks up asset sales and purchases, with large volumes trading in automated
market making venues such as Uniswap or Curve. Issues arise with this
automation, as decentralized finance operators are aware of Just-In-Time
liquidity bots that serve to siphon MEV. Another factor are yield farming
operations where protocols give additional value to market makers for providing
token liquidity, giving rise to "mercinary capital" which may easily pull
liquiditiy before market events occur. Because of these factors, it is unknown
in general at any given time how much liquidity is available if a collateral
shock occurs since these market making operations, whether automated or just in
time, are not obligated to be available during market downturns.

While lending operators can take into account liquidity available on
decentralized exchanges, it should serve no surprise that under a market shock,
the available market makers can and will pull their liquidity from the market.
The understanding of liquidity has a direct effect on volatility as it would be
captured in returns as long as samples cover market shocks, which may lead
lending practitioners to be wary of available liqudiity and volatility metrics
when considering lending agreements. Also, it may benefit lending protocols to
also engage in market making, and provide rewards and other equity returns to
participants to soak downward pricing in collateral auctions, effectively
engaging in a risk swap to offset potential losses.

# Final Thoughts

Risk assessments in crypto credit markets is a relatively new field with many
hurdles to overcome. While the space does have high volatility, there is still
much to be considered as the blockchain space is a data rich environment. This
document lighted VAR/Volatility, the Merton Default Probability Model, and Risk
tranches as possible options for credit risk assessments that ultimately
determine lending rates. While these should be considered as a first step,
jhere is no shortage of new metrics to add to a panel of risk indicators, and
lots of opportunities.

Along with this and the advent of the blockchain and AI systems, there are
deeper risk modeling considerations that may be worth exploring for more well
capitalized teams focused on assessing credit risk, and building quantitative
risk systems. Prudent lending protocol users interested in risk frameworks
should consider these basic options as a start. Operators engaging in DeFi
lending markets should take these as baseline requirements at the start, and
work to engineer their own in house automated risk operations.

