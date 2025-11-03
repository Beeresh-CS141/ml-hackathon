# Improved HMM Results

## Overview
This document summarizes the results of the Improved HMM implementation that enhances the baseline HMM approach with N-gram transition probabilities.

## Performance Comparison

| Method | Success Rate | Final Score | Improvement |
|--------|--------------|-------------|-------------|
| **Original HMM** | 19.80% | -55,324 | Baseline |
| **RL + HMM** | 19.90% | -55,302 | +0.5% |
| **Improved HMM** | **24.60%** | **-53,878** | **+24.2%** |
| **Enhanced N-gram** | 35.70% | -50,471 | Best overall (non-HMM) |

## Key Improvements

### 1. **Transition Probabilities**
The Improved HMM adds transition probabilities to the baseline emission-based HMM:
- **Bigram transitions**: P(letter_i+1 | letter_i) - 676 unique pairs
- **Trigram transitions**: P(letter_i+2 | letter_i, letter_i+1) - 8,148 unique sequences

### 2. **Enhanced Emission Probabilities**
- Position-based letter frequencies with Laplace smoothing
- Adaptive smoothing parameter (α = 0.1)
- Handles unseen word lengths gracefully

### 3. **Adaptive Weighting Strategy**
The model adjusts weights based on game progress:

**Early Game (<20% revealed):**
- Emission: 60%, Bigram: 20%, Trigram: 10%, Global: 10%
- Focus on positional patterns

**Mid Game (20-50% revealed):**
- Emission: 40%, Bigram: 30%, Trigram: 20%, Global: 10%
- Balance between position and context

**Late Game (>50% revealed):**
- Emission: 20%, Bigram: 30%, Trigram: 40%, Global: 10%
- Emphasize sequential patterns

### 4. **Conservative Strategy**
- Prioritize vowels (e, a, i, o, u) in early game
- Switch to consonants after common vowels tried
- Maintain guessing order based on probability when lives ≤ 2

## Achievements

✓ **24.2% relative improvement** over baseline HMM (19.8% → 24.6%)  
✓ **1,446 points improvement** in final score (-55,324 → -53,878)  
✓ **Maintains HMM framework** while adding transition probabilities  
✓ **Proper probabilistic approach** using emission + transition models

## Why This Improvement Matters

1. **Validates HMM Enhancement**: Shows that adding transition probabilities to HMM significantly improves performance
2. **Maintains Project Requirements**: Still uses HMM methodology (emission + transition probabilities)
3. **Substantial Gains**: Nearly 5% absolute improvement is significant for this task
4. **Room for Growth**: While Enhanced N-gram (35.7%) performs better, Improved HMM demonstrates the potential of HMM-based approaches

## Sample Test Results

**Test on 5 random words:**
- **marmar**: WON (1 wrong guess)
- **janet**: LOST (6 wrong guesses)
- **dentistical**: WON (3 wrong guesses)
- **troveless**: WON (3 wrong guesses)
- **unnotify**: LOST (6 wrong guesses)

**Win rate on samples**: 60% (3/5)

## Technical Details

**Training Data:**
- 49,954 corpus words (49,375 unique)
- 0 overlap with test set

**Test Data:**
- 2,000 test words (all unique)

**Model Components:**
- 23 word length categories
- 676 bigram transition pairs
- 8,148 trigram transition sequences
- Position-based emission probabilities for all lengths

**Evaluation Metrics:**
- Total games: 2,000
- Wins: 492 (24.60%)
- Total wrong guesses: 10,874
- Average wrong guesses: 5.437
- Final score: -53,878

## Conclusion

The Improved HMM successfully demonstrates that:
1. Adding transition probabilities to HMM emission models improves performance
2. Context-aware predictions (bigrams/trigrams) help in letter guessing
3. Adaptive weighting based on game state enhances decision-making
4. HMM methodology can be extended while maintaining its probabilistic foundation

While the Enhanced N-gram model (35.70%) outperforms all HMM-based approaches, the Improved HMM shows substantial gains over the baseline and validates the effectiveness of proper HMM enhancements.

---
**Project**: ML Hackathon - Hangman AI (UE23CS352A)  
**Date**: 2024  
**Model**: Improved HMM with N-gram Transitions
