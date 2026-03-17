# BIT-170326: Staking to Cold Key

- **BIT Number:** 170326
- **Title:** Staking to Cold Key
- **Author(s):** CapriciousSage
- **Discussions-to:** CoR OpenDev
- **Status:** Draft
- **Type:** Core
- **Created:** 17/03/2026
- **Updated:** 17/03/2026
- **Requires:** N/A
- **Replaces:** N/A

## Abstract

Rework Staking and Child Hotkey (CHK) Staking to associate with the (singular) Validator Cold Key / Identity, instead of split across the (up to 129 per Validator) Hotkeys.

![BIT-170326 - Figure 01](https://raw.githubusercontent.com/CapriciousSage/bits/refs/heads/main/bits/BIT-170326-01.png)

## Motivation

The current structure is a Band-Aid on a Band-Aid. Validators currently have a "root" hotkey (that does not run any code), with actual infrastructure operations split across a separate hotkey for each subnet. Delegate stake is split between the root and subnet specific keys, while CHK Stake is attached to each of the individual subnet keys. 

## Specification

First Described in [Issue 1620](https://github.com/opentensor/subtensor/issues/1620), this process involves a few steps.
- The technical implementation of associating Root, dTAO and CHK Stake with the Cold Key 
- Coordinated global migration of all existing stake from Hotkeys to the Cold Key 
- Restricting Hotkey Registration to one UID per Subnet per Cold Key
- Coordinated Updates on Front End and Wallet Apps 

## Rationale

The current setup results in poor user experience, messy front ends, complicated reporting, varied APYs (due to CHK Take only applying to stake on the subnet specific key), slow adaptability in the event of validator technical issues, and incorrect reporting for the upcoming governance features. The only players that benefit from the current mess are CHK/Weight Copy Validators that benefit from having all of their weight focused on a single key, while Infra Valis continue to suffer.

## Backwards Compatibility

After the switch, there needs to be one of two backwards compatibility considerations:
a) Clear error messages explaining that the user must stake to the Coldkey instead
b) Automated remapping of any staking attempts to a hotkey across to the correct Coldkey  

## Security Considerations

To prevent abuse, it is imperative that either Hotkey Registrations be limited to one UID per Subnet per Hotkey, or at the very least, limiting vTrust to only one hotkey per subnet per Cold key. The former is suggested as it eliminates more potential edge case scenarios.

## Copyright

This document is licensed under [The Unlicense](https://unlicense.org/).
