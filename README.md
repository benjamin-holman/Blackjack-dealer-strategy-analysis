# Blackjack Dealer Analysis

Monte Carlo analysis of blackjack in Python. The casino fixes the dealer's rule (stand on 17) and players then choose their strategy, so this is a leader–follower game. The question: given that players respond with their best strategy, does stand-on-17 maximise the house edge?

## Method
- Infinite deck: each rank drawn with probability 1/13 (10-value cards 4/13)
- Aces count as 11, reduced to 1 if the hand would bust
- Dealer stands on 17 (including soft 17) unless stated
- Blackjack pays 3:2; a dealer blackjack beats any player hand except a player blackjack
- 1,000,000 simulated hands per result

## 1. Dealer final totals by stopping threshold

| Final total | Stand 15 | Stand 16 | Stand 17 | Stand 18 | Stand 19 | Stand 20 |
|---|---|---|---|---|---|---|
| 15 | 13.30% | | | | | |
| 16 | 12.73% | 13.89% | | | | |
| 17 | 12.23% | 13.35% | 14.53% | | | |
| 18 | 11.70% | 12.79% | 13.92% | 15.15% | | |
| 19 | 11.13% | 12.23% | 13.24% | 14.60% | 15.86% | |
| 20 | 15.81% | 16.84% | 18.09% | 19.24% | 20.56% | 21.98% |
| 21 | 5.03% | 6.11% | 7.26% | 8.50% | 9.78% | 11.22% |
| Blackjack | 4.74% | 4.71% | 4.73% | 4.75% | 4.75% | 4.74% |
| **Bust** | **13.33%** | **20.08%** | **28.22%** | **37.75%** | **49.05%** | **62.06%** |

Stand-on-17 results match published figures (bust ≈ 28%). Blackjack frequency is constant (≈ 8/169 = 4.73%) since it depends only on the first two cards.

## 2. House edge when the player copies the dealer
The player hits until reaching the same threshold as the dealer. The only asymmetries: **the player acts first and loses immediately on a bust, even if the dealer would also have bust**, and a player blackjack pays 3:2.

| Shared threshold | House edge |
|---|---|
| 15 | −0.49% |
| 16 | +1.87% |
| 17 | +5.85% |
| 18 | +11.93% |
| 19 | +21.67% |
| 20 | +36.31% |

At the casino standard of 17, copying the dealer gives the house about a 5.9% edge (published figure ≈ 5.5%), entirely from the bust asymmetry. At 15, busts are rare enough that the 3:2 blackjack bonus gives the player a slight edge.

## 3. Player best response
*(in progress: dealer fixed at 17, player threshold varied 12–20)*
