---
sidebar_position: 2
---

# Darwinia Chain Parameters

> This page intends to reflect the current configurations of the Darwinia mainnet and provide some brief explanation to their meanings when necessary.

## Periods of Common Actions and Attributes

Following are the definitions of the three mostly widely used time periods in Darwinia.

| Darwinia | Time      | Slots |
| -------- | --------- | ----- |
| Block    | 6 seconds | 1     |
| Epoch    | 4 hour    | 2,400 |
| Era      | 24 hours  |14,400 |


## Current Seats(Jun 2022)
Following are the numbers of members in difference organizations(sets) in Darwinia. These numbers are not fixed. They may be changed over time by on-chain governance.

| Organization | Seats  |
| -------- | --------- |
| Validators   | 105 |
| Council    | 7    |
| Technical committee | 5  |

## Staking, Validating, and Nominating
Following are the configuration of the lengths of time periods in Darwinia.

| Darwinia                | Time                               | Slots                                                      | Description                                                                                                                                      |
| ----------------------- | ---------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Term duration           | 24 hours                            | 14,400                                                      | The time for which a validator is in the set after being elected. Note,  this duration can be shortened in the case that a validator misbehaves. |
| Nomination period       | 24 hours                            | 14,400                                                      | Every 24 hours, a new validator set is elected according to Phragmen's method.                                                                    |
| Bonding duration        | 14 days                            | 201,600                                                    | How long until your funds will be transferable after unbonding.                                                                                 |
                                                             
## Parameters of Validators
One preliminary method to make profit is to nominate a validator. There are multiple factors to consider when choosing a validator wisely. Although we do not make recommendations out of neutrality, we provide an explanation of the meaning of the parameters related to a validator. A comprehensive understanding can help you assess your candidates accurately.

### Active Commission
The *active commission* is the percentage of the gain that the validator will draw before distributing according to staking power in the current era. This parameter is set by the validator. From one perspective, it measures the willingness of the validator to share the profit with nominators. Meanwhile, it can be interpreted as an indicator of their confidence in themselves. In a nutshell, one cannot say that the higher the better or otherwise.

### Next Commission
The *next commission* is the percentage of the gain that the validator will draw before distributing according to staking power in the next era. This parameter is set by the validator. It may directly affect your profit if you endorse this validator. As explained above, this is not a simple measure of good or bad.

### Own Stake(Power)
The *own stake (power)* is the amount of power that the validator has locked for staking currently. It indicates how much stake the validator has put in the game. Since if the validator is punished for some reason, part of the staking power will be slashed, the higher this number is, the higher risk the validator is willing to take.

### Other Stake(Power)
The *other stake (power)* is the amount of power that nominators have trusted the validator with. This partly indicates the level of confidence that nominators have on the validator.

### Points
The *point* is a measure of the validator's achievement in the current era. The validator normally gets 20 points for each block produced by them. If a validator has 1200 *points*, it means that this validator has produced 60(=1200/20) blocks successfully so far in current era.