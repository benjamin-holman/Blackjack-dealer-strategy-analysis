# Blackjack Dealer Analysis

Probability analysis of blackjack in Python with Monte Carlo simulations used to verify results. 
The casino fixes the dealer's rule (stand on 17) and players then choose their strategy, so this is a leader–follower game. 
We want to find if given that players respond with their best strategy, does stand-on-17 maximise the house edge?
For this we look at a very basic version of player strategy, they pick a threshold and hit until they reach it.

## Method
- Infinite deck: each rank drawn with probability 1/13 (10-value cards 4/13)
- Aces count as 11, reduced to 1 if the hand would bust
- Dealer stands on 17 (including soft 17) unless stated
- Blackjack pays 3:2; a dealer blackjack beats any player hand except a player blackjack
- Main results are computed exactly
- Each result is verified by Monte Carlo simulations (1,000,000 simulations)


## Results
- Against a player using their best fixed threshold, standing on 17 maximises the house edge (5.21%)
- Against a best-responding player, the house only has a positive edge when the dealer stands on 16 or 17


## 1. Dealer final totals by stopping threshold

Solving exactly
| Final total | Stand 15 | Stand 16 | Stand 17 | Stand 18 | Stand 19 | Stand 20 |
|---|---|---|---|---|---|---|
| 15 | 13.29% | | | | | |
| 16 | 12.80% | 13.88% | | | | |
| 17 | 12.27% | 13.36% | 14.51% | | | |
| 18 | 11.71% | 12.8% | 13.95% | 15.18% | | |
| 19 | 11.11% | 12.19% | 13.35% | 14.57% | 15.88% | |
| 20 | 15.78% | 16.87% | 18.03% | 19.25% | 20.56% | 21.96% |
| 21 | 5.03% | 6.12% | 7.27% | 8.50% | 9.81% | 11.2% |
| Blackjack | 4.73% | 4.73% | 4.73% | 4.73% | 4.73% | 4.73% |
| **Bust** | **13.28%** | **20.04%** | **28.16%** | **37.77%** | **49.02%** | **62.11%** |

Monte Carlo simulation with 1,000,000 simulations
| Final total | Stand 15 | Stand 16 | Stand 17 | Stand 18 | Stand 19 | Stand 20 |
|---|---|---|---|---|---|---|
| 15 | 13.28% | | | | | |
| 16 | 12.77% | 13.89% | | | | |
| 17 | 12.31% | 13.27% | 14.47% | | | |
| 18 | 11.75% | 12.79% | 13.95% | 15.17% | | |
| 19 | 11.10% | 12.19% | 13.31% | 14.57% | 15.89% | |
| 20 | 15.70% | 16.92% | 18.02% | 19.24% | 20.56% | 22.02% |
| 21 | 5.04% | 6.13% | 7.29% | 8.49% | 9.82% | 11.17% |
| Blackjack | 4.74% | 4.76% | 4.76% | 4.74% | 4.74% | 4.73% |
| **Bust** | **13.31%** | **20.05%** | **28.20%** | **37.8%** | **48.98%** | **62.08%** |



## 2. House edge when the player copies the dealer
The player hits until reaching the same threshold as the dealer. A player blackjack pays 3:2.

Solving exactly 
| Shared threshold | House edge |
|---|---|
| 15 | −0.49% |
| 16 | +1.76% |
| 17 | +5.67% |
| 18 | +12.01% |
| 19 | +21.78% |
| 20 | +36.32% |

Monte Carlo simulations with 1,000,000 simulations
| Shared threshold | House edge |
|---|---|
| 15 | −0.54% |
| 16 | +1.67% |
| 17 | +5.61% |
| 18 | +12.05% |
| 19 | +21.82% |
| 20 | +36.4% |

At the casino standard of 17, copying the dealer gives the house a 5.67% edge.
At 15, busts are rare enough that the 3:2 blackjack bonus gives the player a slight edge.

## 3. Player's best response
For each dealer stopping threshold from 15-20 the player will pick their threshold to be the best response.

Solving exactly
| Player stands on | Dealer 15 | Dealer 16 | Dealer 17 | Dealer 18 | Dealer 19 | Dealer 20 |
|---|---|---|---|---|---|---|
| 12 | 13.70 | 12.81 | 8.08 | −0.93 | −14.73 | −33.85 |
| 13 | 9.16 | 9.91 | 6.82 | −0.57 | −12.77 | −30.36 |
| 14 | 4.34 | 6.99 | 5.82 | 0.36 | −9.94 | −25.65 |
| 15 | −0.49 | 4.27 | 5.28 | 2.01 | −6.07 | −19.58 |
| 16 | −3.46 | 1.76 | 5.21 | 4.46 | −1.08 | −12.01 |
| 17 | −2.31 | 1.57 | 5.67 | 7.76 | 5.14 | −2.82 |
| 18 | 3.50 | 6.17 | 9.00 | 12.01 | 12.71 | 8.17 |
| 19 | 14.57 | 16.21 | 17.95 | 19.80 | 21.78 | 21.14 |
| 20 | 31.56 | 32.40 | 33.29 | 34.23 | 35.24 | 36.32 |

Player's best response 

| Dealer stands on | Best player threshold | House edge (%) |
|---|---|---|
| 15 | 16 | −3.46 |
| 16 | 17 | 1.57 |
| 17 | 16 | 5.21 |
| 18 | 12 | −0.93 |
| 19 | 12 | −14.73 |
| 20 | 12 | −33.85 |

We see that the diagonal (where the player threshold is the same as the dealer threshold) matches our results from part 2 which helps verify the results.
We see that dealer standing at 17 gives the casino the highest house edge if players are playing optimally.

Monte carlo simulation 
| Player stands on | Dealer 15 | Dealer 16 | Dealer 17 | Dealer 18 | Dealer 19 | Dealer 20 |
|---|---|---|---|---|---|---|
| 12 | 13.76 | 12.87 | 7.93 | −0.96 | −14.73 | −33.80 |
| 13 | 9.22 | 9.92 | 6.80 | −0.51 | −12.73 | −30.36 |
| 14 | 4.59 | 6.91 | 5.83 | 0.35 | −9.84 | −25.77 |
| 15 | −0.56 | 4.22 | 5.09 | 2.02 | −6.11 | −19.68 |
| 16 | −3.36 | 1.74 | 5.13 | 4.40 | −0.98 | −11.86 |
| 17 | −2.10 | 1.56 | 5.75 | 7.74 | 5.06 | −2.70 |
| 18 | 3.62 | 6.38 | 8.97 | 11.95 | 12.86 | 8.35 |
| 19 | 14.52 | 16.29 | 17.92 | 19.84 | 21.83 | 21.06 |
| 20 | 31.60 | 32.46 | 33.22 | 34.22 | 35.26 | 36.23 |

| Dealer stands on | Exact best response | Simulated best response |
|---|---|---|
| 15 | 16 (−3.46%) | 16 (−3.36%) |
| 16 | 17 (1.57%) | 17 (1.56%) |
| 17 | 16 (5.21%) | 15 (5.09%) |
| 18 | 12 (−0.93%) | 12 (−0.96%) |
| 19 | 12 (−14.73%) | 12 (−14.73%) |
| 20 | 12 (−33.85%) | 12 (−33.80%) |

The simulation recovers the same best response for five of the six dealer rules. 
Against dealer 17 it selects 15 rather than 16: the exact gap is only 0.07 percentage points, below the ~0.2-point simulation error.
This is why the exact method is used for the final results.

## Limitations and next steps
- Players are restricted to stopping thresholds and do not use the information of the dealer's up-card.
- Doubling and splitting are not considered which would reduce the house edge.
- The infinite-deck assumption removes card-removal effects. A finite shoe would allow analysis of card counting.
- Next step: an up-card-dependent strategy, computing the player's best threshold for each dealer up-card.
