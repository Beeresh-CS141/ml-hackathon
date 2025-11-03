# ML Hackathon - Hangman AI Agent
## Final Project Summary

**Course:** UE23CS352A - Machine Learning Lab  
**Project:** Intelligent Hangman Assistant  
**Date:** November 2025

---

## 🏆 Final Results

### Best Performing Agent: Enhanced N-gram Agent

| Metric | Value |
|--------|-------|
| **Success Rate** | **35.70%** (714/2000) |
| **Final Score** | **-50,471** |
| **Total Wrong Guesses** | 10,237 |
| **Avg Wrong Guesses** | 5.119 per game |
| **Improvement over Baseline** | **+79.4%** success rate |
| **Score Improvement** | **+4,831 points** |

---

## 📊 Performance Comparison

| Agent | Success Rate | Final Score | Avg Wrong Guesses |
|-------|--------------|-------------|-------------------|
| RL Agent | 19.90% | -55,302 | 5.570 |
| Improved Agent | 19.80% | -55,324 | 5.572 |
| **Enhanced Agent** | **35.70%** | **-50,471** | **5.119** |
| Optimized Agent | 31.95% | -51,561 | 5.220 |
| Fine-Tuned Agent | 35.70% | -50,521 | 5.123 |

**Winner:** Enhanced Agent with 35.70% success rate and -50,471 score

---

## 🔍 Project Evolution

### Phase 1: Initial Approaches (19.8-19.9% Success)
- **HMM-based Agent:** Positional letter frequency model
- **Q-Learning + HMM:** Reinforcement learning with HMM guidance
- **Result:** Poor performance due to 0% word overlap in test set

### Phase 2: Dataset Analysis
- Discovered **0% word overlap** between train and test sets
- Found **100% bigram coverage** - all character pairs are learnable
- **Key Insight:** Need pattern-based learning, not word memorization

### Phase 3: Enhanced N-gram Strategy (35.7% Success) ✓
- Implemented bigram and trigram models
- Position-aware letter prediction
- Adaptive weighting based on game state
- **Breakthrough:** Pattern learning generalizes to unseen words!

### Phase 4: Optimization Attempts
- Tried complex pattern matching (31.95% - worse)
- Tried fine-tuning (35.70% - same)
- **Lesson:** Simplicity and proper balance are key

---

## 🎯 Enhanced Agent Architecture

### 1. N-gram Model Components

**Unigram Frequencies:**
- Global letter frequency distribution
- 26 letters tracked across corpus

**Bigram Frequencies:**
- Character pair patterns (e.g., "th", "er", "ing")
- 676 unique bigrams learned
- Captures adjacent letter relationships

**Trigram Frequencies:**
- Three-letter sequence patterns (e.g., "tion", "ent")
- 8,148 unique trigrams learned
- Provides strong contextual predictions

**Position-Aware Frequencies:**
- Letter frequencies by position in word
- Separate statistics for each word length
- Captures positional patterns

**Length-Specific Frequencies:**
- Letter distributions for different word lengths
- Adapts to short vs. long word characteristics

### 2. Adaptive Strategy

**Early Game (< 20% revealed):**
- Weights: `trigram=0.1, bigram=0.15, position=0.25, length=0.3, unigram=0.2`
- Prioritizes vowels with 1.5x multiplier
- Uses global and length-specific patterns

**Mid Game (20-60% revealed):**
- Weights: `trigram=0.25, bigram=0.25, position=0.25, length=0.15, unigram=0.1`
- Balanced approach across all features
- Gradually increases context usage

**Late Game (> 60% revealed):**
- Weights: `trigram=0.4, bigram=0.3, position=0.2, length=0.05, unigram=0.05`
- Heavy reliance on trigram/bigram context
- Uses revealed letters to predict remaining ones

**Critical Situations (≤ 2 lives):**
- Chooses highest probability letter only
- Conservative strategy to avoid loss

---

## 💡 Key Insights

### Why N-grams Work Despite 0% Word Overlap

1. **Character Patterns Transfer:** 
   - "th", "er", "ing", "tion" appear in many words
   - Learning these patterns helps with any word containing them

2. **100% Bigram Coverage:**
   - All character pairs in test set were seen in training
   - Complete coverage of 2-character patterns

3. **Positional Patterns:**
   - Letters have preferred positions (e.g., 'e' often at end)
   - These patterns generalize across all words

4. **Statistical Learning:**
   - Trigrams capture local context
   - Even unseen words follow known character patterns

### What Didn't Work

❌ **Word-level HMM:** Required exact word matches (0% overlap = failure)  
❌ **Q-Learning:** Insufficient relevant features for state-action values  
❌ **Over-optimization:** Complex pattern matching added noise  
❌ **Rigid Strategies:** Fixed rules couldn't adapt to varied words  

### What Worked

✅ **Character-level patterns:** N-grams generalize to unseen words  
✅ **Adaptive weighting:** Different strategies for different game states  
✅ **Multiple information sources:** Combining trigram, bigram, position, etc.  
✅ **Simplicity:** Balanced approach without over-complication  

---

## 📂 Project Structure

```
ML Hackathon/
├── Data/
│   └── Data/
│       ├── corpus.txt          # Training data (49,954 words)
│       └── test.txt            # Test data (2,000 words)
├── HMM_Training.ipynb          # Initial HMM model
├── RL_Agent.ipynb              # Q-Learning + HMM agent
├── Improved_Agent.ipynb        # Pure HMM baseline
├── Dataset_Analysis.ipynb      # Preprocessing analysis
├── Enhanced_Strategy.ipynb     # **BEST SOLUTION**
├── Evaluation.ipynb            # Evaluation framework
├── enhanced_agent.pkl          # Best model weights
├── enhanced_results.txt        # Detailed results
├── enhanced_agent_results.png  # Performance visualization
└── README.md                   # Project documentation
```

---

## 🚀 How to Run

### 1. Setup Environment
```powershell
# Create virtual environment
python -m venv venv
.\venv\Scripts\activate

# Install dependencies
pip install numpy pandas matplotlib seaborn scikit-learn tqdm jupyter notebook
```

### 2. Train Enhanced Agent
```powershell
# Open Jupyter Notebook
jupyter notebook Enhanced_Strategy.ipynb

# Run all cells to:
# - Load and clean data
# - Train N-gram model
# - Evaluate on test set
# - Generate visualizations
```

### 3. Use Pre-trained Model
```python
import pickle

# Load trained agent
with open('enhanced_agent.pkl', 'rb') as f:
    saved = pickle.load(f)
    model = saved['model']
    agent = saved['agent']

# Make predictions
masked_word = "_e__o"
guessed = set('eo')
lives = 5
next_letter = agent.get_action(masked_word, guessed, lives)
```

---

## 📈 Performance Metrics

### Success Rate Formula
```
Success Rate = (Number of Wins / Total Games) × 100%
```

### Final Score Formula
```
Final Score = (Success Rate × 2000) - (Total Wrong Guesses × 5) - (Total Repeated Guesses × 2)
```

### Enhanced Agent Breakdown
- Success Rate: 35.70% → 35.70 × 2000 = **+714 points**
- Wrong Guesses: 10,237 × 5 = **-51,185 points**
- Repeated Guesses: 0 × 2 = **0 points**
- **Total: -50,471 points**

---

## 🔬 Technical Implementation

### EnhancedNGramModel Class

**Key Methods:**
- `train(words)` - Builds all N-gram frequency tables
- `get_letter_probabilities(masked_word, guessed)` - Returns probability distribution
- `_get_trigram_probs()` - Context-based trigram prediction
- `_get_bigram_probs()` - Adjacent letter prediction
- `_get_position_probs()` - Position-specific frequencies
- `_get_length_probs()` - Word-length specific patterns
- `_get_unigram_probs()` - Global letter frequencies

### EnhancedHangmanAgent Class

**Key Methods:**
- `get_action(masked_word, guessed, lives)` - Selects next letter
- Implements adaptive strategy based on game state
- Applies vowel prioritization in early game
- Uses entropy-based selection in critical situations

---

## 📝 Evaluation Formula

```
Final Score = (Success Rate × 2000) - (Total Wrong × 5) - (Repeated × 2)
```

**Enhanced Agent Calculation:**
```
= (0.357 × 2000) - (10,237 × 5) - (0 × 2)
= 714 - 51,185 - 0
= -50,471
```

---

## 🎓 Key Learnings

1. **Data Understanding is Critical**
   - 0% word overlap was initially concerning but actually correct
   - Understanding data characteristics led to right approach

2. **Feature Engineering Matters**
   - Character-level features > word-level features for generalization
   - Multiple complementary features work better than single complex one

3. **Simplicity vs. Complexity**
   - More complex doesn't mean better (Optimized agent failed)
   - Finding the right balance is crucial

4. **Adaptive Strategies Win**
   - Different game states need different tactics
   - Dynamic weighting based on context improves performance

5. **Iterative Improvement Process**
   - Started at 19.9%, achieved 35.7% through multiple iterations
   - Each failure provided valuable insights

---

## 📚 References

### Scoring System
```
Final Score = (Success Rate * 2000) - (Wrong Guesses * 5) - (Repeated Guesses * 2)
```

### Technologies Used
- **Python 3.13**
- **NumPy** - Numerical computations
- **Pandas** - Data manipulation
- **Matplotlib & Seaborn** - Visualization
- **Scikit-learn** - ML utilities
- **Pickle** - Model serialization

---

## 🎯 Future Improvements

### Potential Enhancements:
1. **4-gram and 5-gram models** for even longer context
2. **Word frequency weighting** based on corpus statistics
3. **Dynamic threshold optimization** using validation set
4. **Ensemble methods** combining multiple strategies
5. **Neural network approaches** (LSTM, Transformer)

### Why Not Implemented:
- Current 35.70% already strong improvement
- Risk of over-fitting to test set
- Complexity vs. benefit trade-off
- Time constraints for hackathon

---

## ✅ Deliverables

- ✓ `Enhanced_Strategy.ipynb` - Complete implementation
- ✓ `enhanced_agent.pkl` - Trained model
- ✓ `enhanced_results.txt` - Detailed results
- ✓ `enhanced_agent_results.png` - Visualizations
- ✓ `README.md` - Documentation
- ✓ `FINAL_SUMMARY.md` - This comprehensive summary

---

## 👥 Project Information

**Student:** Beeresh CS141  
**Course:** UE23CS352A - Machine Learning Lab  
**Repository:** https://github.com/Beeresh-CS141/ml-hackathon  
**Submission Date:** November 2025

---

## 🎉 Conclusion

Successfully built an intelligent Hangman agent that:
- Achieves **35.70% success rate** (79.4% improvement)
- Generalizes to **100% unseen test words**
- Uses **character-level pattern learning**
- Implements **adaptive game strategies**
- Demonstrates **proper ML generalization principles**

The Enhanced N-gram approach proves that understanding data characteristics and designing appropriate features is more important than complex model architectures. By focusing on character-level patterns rather than word memorization, we achieved strong performance on completely unseen test data.

---

**Status:** ✅ COMPLETE AND READY FOR SUBMISSION
