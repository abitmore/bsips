    BSIP: TBD
    Title: Share market fees to the network
    Author: Abit More <https://github.com/abitmore>
    Status: Draft
    Type: Protocol
    Created: 2019-11-29
    Discussion: https://github.com/bitshares/bsips/issues/194
    Worker: TBD

# Abstract

This BSIP proposes a protocol change: when every trade happens, if there are
market fees generated, a portion (E.G. 5% or 10%) of the market fees goes to
the network.

# Motivation

The network needs more tools to generate income to support its development.

# Rationale

A major activity in the network is trading assets. The asset owners make
profits in the form of market trading fees. Currently, the main tools for the
network to generate income from asset trading activities are order creation
fee and order cancellation fee. It seems reasonable that the asset owners
share some profits (a part of market fees) to the network to support its
development.

The cut of market fees can go to committee-account's vesting balances.
As a supporting measure, committee-account should be exempted from
white-listing restrictions, so that it is able to claim the vesting balances
and sell them for core token or other tokens to pay for development later.

# Specifications

## Protocol upgrade

A time will need to be scheduled for applying the change. In this document,
terms "before the protocol upgrade", "at the protocol upgrade" and "after
the protocol upgrade" may or may not be used to indicate things happen before
the scheduled time, at the scheduled time and after the scheduled time.

## New global parameter

Add a new global parameter `market_fee_network_percent` which can be updated
by the committee only after the protocol upgrade.
Initial value of that parameter is `0`.
Valid range of that parameter is `[0, 100%]`.

## When processing market fees

After the protocol upgrade, when splitting a non-zero market fee, firstly
split `amount * market_fee_network_percent` (round down) to committee-account,
then process the remainder as before. The amount split to committee-account
should go to the vesting balance object whose type is `market_fee_sharing`.

## When checking asset authorities

After the protocol upgrade, when checking authorities (E.G. white-lists) of an
asset on an account, if the account is committee-account, let it pass.

# Discussion

* Other than [the "coin-days as market fees" proposal](
 https://github.com/bitshares/bsips/issues/191) which applies
 a discount to market fees to benefit core token holders directly, this BSIP
 seeks for a mechanism to increase the network's income and benefit core token
 holders indirectly.

* Adjusting the fee schedule and network percent in the referral program is
 another option to increase the network's income, and is probably sufficient
 for funding development.

* In the original design, the purpose of market fees is to reward asset
 issuers for their work (e.g. gateway providers, or businesses built around
 PMs), while operation fees (`limit_order_create/cancel` in particular) reward
 the network for performing its work. The separation of market/operation fees
 matches the separation of roles. Changing this may damage existing businesses.
 Thus this BSIP could be a bad idea from this perspective. Also note that the
 network can profit from market fees by setting them on committee-owned tokens.

* This would be another motivation for businesses building on top of BitShares
 to get involved in the parameter governance process. The percentage can be
 `0` if it's more appropriate.

* Asset owners can specify a zero market fee percentage to get around the
 "tax", while still profiting by setting a higher deposit/withdrawal fee.
 It is uncommon nowadays probably because it's less convenient or attractive
 for their customers.

* Another strategy is to charge a network market fee globally, independent of
 what the asset owner decides. It essentially removes the option to not set
 a fee from asset owners, which kills some freedom and would hinder non-profit
 use of the platform.

* It's possible that committe-account would accumulate a lot of tokens with no
 value and tokens which are unable or hard to be used to pay for development.
 It's a side effect. Hopefully there will be quite some usable tokens.
 The committee will have to do some work to manage the tokens anyway.

# Non-Technical Summary

This BSIP adds a tool for the committee to impose a tax on market trading
fees for all assets which enabled market trading fee, thus would potentially
increase income for the network to support its development. It may probably
damage businesses relying on market fees if the committee-decided tax is high.
The committee may need some efforts to manage the income.

# Copyright

This document is placed in the public domain.

# See Also

* https://github.com/bitshares/bsips/issues/194