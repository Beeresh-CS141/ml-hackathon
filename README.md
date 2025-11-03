# Intelligent Hangman Agent - ML Hackathon

**Course:** UE23CS352A - Machine Learning Lab  
**Project:** Intelligent Hangman Assistant  
**Author:** Beeresh CS141  
**Date:** November 2025

---

## 🏆 Final Results - Best Solution

### Enhanced N-gram Agent Performance

| Metric | Value |
|--------|-------|
| **Success Rate** | **35.70%** (714/2000 wins) |
| **Final Score** | **-50,471** |
| **Total Wrong Guesses** | 10,237 |
| **Avg Wrong Guesses** | 5.119 per game |
| **Improvement over Baseline** | **+79.4%** success rate |
| **Score Improvement** | **+4,831 points** |

---

## 📊 All Approaches Comparison

| Agent | Success Rate | Final Score | Avg Wrong | Status |
|-------|--------------|-------------|-----------|---------|
| Original HMM | 19.80% | -55,324 | 5.572 | HMM Baseline |
| RL + HMM | 19.90% | -55,302 | 5.570 | Hybrid Approach |
| **Improved HMM** | **24.60%** | **-53,878** | **5.437** | ✅ **+24% over HMM** |
| **Enhanced N-gram** | **35.70%** | **-50,471** | **5.119** | ✅ **BEST OVERALL** |
| Optimized N-gram | 31.95% | -51,561 | 5.220 | Over-complicated |
| Fine-Tuned N-gram | 35.70% | -50,521 | 5.123 | Same as Enhanced |

---

## 🚀 Quick Start

### 1. Setup Environment
```powershell
cd "ML Hackathon"
python -m venv venv
.\venv\Scripts\activate
pip install numpy pandas matplotlib seaborn scikit-learn tqdm jupyter notebook
```

### 2. Run Best Solution
```powershell
jupyter notebook Enhanced_Strategy.ipynb
# Run all cells to train and evaluate
```

---

## 📁 Project Structure

```
ML Hackathon/
├── Data/Data/
│   ├── corpus.txt                 # 49,954 training words
│   └── test.txt                   # 2,000 test words
├── Enhanced_Strategy.ipynb        # 🏆 BEST SOLUTION (35.7%)
├── Improved_HMM.ipynb             # ✅ Enhanced HMM (24.6%)
├── Dataset_Analysis.ipynb         # Data preprocessing
├── HMM_Training.ipynb             # HMM baseline (19.8%)
├── RL_Agent.ipynb                 # Q-Learning baseline (19.9%)
├── Evaluation.ipynb               # Evaluation framework
├── enhanced_agent.pkl             # Best N-gram model
├── improved_hmm_model.pkl         # Improved HMM model
├── improved_hmm_results.png       # Visualization
├── IMPROVED_HMM_RESULTS.md        # Detailed HMM results
└── README.md                      # This file
```

---

## 🔍 Project Evolution & Key Learnings

### Phase 1: Baseline Approaches (19.8-19.9%)
- **RL + HMM:** 19.90% - Over-relied on Q-table
- **Pure HMM:** 19.80% - Needed exact word matches

### Phase 2: Critical Discovery
- Found **0% word overlap** between train/test
- Found **100% bigram coverage**
- **Insight:** Need character patterns, not word memorization!

### Phase 3: Improved HMM with Transitions (24.6%)
- Added **bigram** and **trigram** transition probabilities to HMM
- Enhanced emission probabilities with Laplace smoothing
- Adaptive weighting based on game state
- **Result:** +24.2% improvement over baseline HMM!

### Phase 4: Enhanced N-gram Solution (35.7%) ✅
- **676 bigrams** + **8,148 trigrams**
- Adaptive weighting by game state
- **Result:** +79.4% improvement over baseline!

### Phase 5: Failed Optimizations
- Over-complicated → worse performance
- **Lesson:** Simplicity wins!

---

## 🧠 How Enhanced Agent Works

### N-gram Components:
- **Unigram:** Global letter frequencies
- **Bigram (676):** Patterns like "th", "er", "ing"
- **Trigram (8,148):** Patterns like "tion", "ent"
- **Position-aware:** Letter frequencies by position
- **Length-specific:** Patterns for different word lengths

### Adaptive Strategy:
```
Early Game (< 20% revealed):  Prioritize vowels, global patterns
Mid Game (20-60%):            Balanced approach
Late Game (> 60%):            Heavy trigram/bigram context
Critical (≤ 2 lives):         Most confident choice only
```

---

## 💡 Why It Works

**Character patterns transfer despite 0% word overlap:**
- Training: "incredible", "kingdom"
- Test: "bringing" (unseen)
- Known patterns: "br", "ing", "gi" → successful prediction!

---

## 📦 Dependencies

```bash
pip install numpy pandas matplotlib seaborn scikit-learn tqdm jupyter notebook
```

---

## ✅ Deliverables

- ✅ `Enhanced_Strategy.ipynb` - Best solution
- ✅ `enhanced_agent.pkl` - Trained model
- ✅ `enhanced_results.txt` - Detailed results
- ✅ `enhanced_agent_results.png` - Visualizations
- ✅ All supporting notebooks and analysis

---

## 🎯 Evaluation Formula

```
Final Score = (Success Rate × 2000) - (Wrong Guesses × 5) - (Repeated Guesses × 2)
= (0.357 × 2000) - (10,237 × 5) - (0 × 2)
= -50,471
```

---

## 🎓 Key Learnings

1. **0% overlap is correct** - Tests true generalization
2. **Character patterns > word memorization**
3. **Adaptive strategies > fixed rules**
4. **Simplicity > over-engineering**
5. **Multiple features provide robustness**

---

## 👥 Project Info

**Repository:** https://github.com/Beeresh-CS141/ml-hackathon  
**Course:** UE23CS352A - Machine Learning Lab  
**Status:** ✅ **COMPLETE**

---

*Last Updated: November 3, 2025*
