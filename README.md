# Intelligent Hangman Agent - ML Hackathon

## Project Overview
This project implements an intelligent Hangman agent using a hybrid approach combining **Hidden Markov Models (HMM)** for pattern recognition and **Reinforcement Learning (RL)** for strategic decision-making.

## 🎯 Challenge
Build an agent that plays Hangman optimally, winning games while minimizing wrong and repeated guesses.

**Evaluation Formula:**
```
Final Score = (Success Rate × 2000) - (Total Wrong Guesses × 5) - (Total Repeated Guesses × 2)
```

## 📁 Project Structure
```
ML Hackathon/
├── Data/
│   └── Data/
│       ├── corpus.txt        # 50,000-word training corpus
│       └── test.txt          # Test words for evaluation
├── HMM_Training.ipynb        # HMM model construction & training
├── RL_Agent.ipynb            # RL environment & agent training
├── Evaluation.ipynb          # Final evaluation on test set
├── hmm_model.pkl             # Trained HMM model (generated)
├── rl_agent.pkl              # Trained RL agent (generated)
├── evaluation_results.txt    # Evaluation results (generated)
├── evaluation_results.png    # Visualization (generated)
└── README.md                 # This file
```

## 🚀 Getting Started

### 1. Setup Virtual Environment
```bash
cd "c:\Users\Beeresha Balegara HT\OneDrive\Desktop\ML Lab\ML Hackathon"
python -m venv venv
.\venv\Scripts\activate
```

### 2. Install Dependencies
```bash
pip install numpy pandas matplotlib seaborn scikit-learn tqdm jupyter notebook
```

### 3. Run the Notebooks (in order)

#### Step 1: Train the HMM
Open and run `HMM_Training.ipynb`:
- Loads the 50,000-word corpus
- Builds positional letter frequency models
- Trains HMM for different word lengths
- Saves trained model as `hmm_model.pkl`

#### Step 2: Train the RL Agent
Open and run `RL_Agent.ipynb`:
- Loads the trained HMM
- Builds the Hangman game environment
- Trains Q-Learning agent using HMM guidance
- Saves trained agent as `rl_agent.pkl`

#### Step 3: Evaluate the Agent
Open and run `Evaluation.ipynb`:
- Loads both trained models
- Evaluates on 2000 test games
- Generates results and visualizations
- Calculates final score

## 🧠 Technical Approach

### Part 1: Hidden Markov Model
**Purpose:** Provide probabilistic letter predictions

**Design Choices:**
- **Hidden States:** Position-specific letter distributions
- **Emissions:** Actual letters at each position
- **Word Length:** Separate models for different lengths
- **Pattern Matching:** Filters corpus words matching current game state

**Key Features:**
- Positional awareness (letters have different probabilities at different positions)
- Fallback mechanisms for unseen patterns
- Efficient word filtering based on masked pattern

### Part 2: Reinforcement Learning Agent
**Algorithm:** Q-Learning with HMM guidance

**State Representation:**
- Masked word (e.g., `_pp__`)
- Set of guessed letters
- Lives remaining
- Word length

**Action Space:**
- 26 possible actions (letters a-z)
- Only unguessed letters are valid

**Reward Function:**
- **+50:** Win the game
- **+2 per letter:** Correct guess (scaled by letters revealed)
- **-10:** Wrong guess
- **-30:** Lose the game
- **-5:** Repeated guess (heavy penalty)

**Decision Strategy:**
- Combines Q-values with HMM probabilities
- ε-greedy exploration (weighted by HMM)
- Action value = Q(s,a) + 10 × P_HMM(a)

## 📊 Expected Results

The agent should achieve:
- **Success Rate:** 70-85% (depending on test set difficulty)
- **Avg Wrong Guesses:** 2-3 per game
- **Minimal Repeated Guesses:** < 0.1 per game
- **Final Score:** 800-1400+ (depending on performance)

## 🔑 Key Insights

### Why This Approach Works:
1. **HMM Provides Domain Knowledge:** Captures English language patterns
2. **RL Learns Strategy:** Optimizes when to trust HMM vs. explore
3. **Hybrid Intelligence:** Better than either approach alone
4. **Efficient Exploration:** HMM-weighted exploration is smarter than random

### Trade-offs:
- **Exploration vs Exploitation:** Balanced with decaying ε-greedy
- **State Space:** Simplified to (pattern, lives, num_guessed) for tractable Q-table
- **Reward Shaping:** Carefully designed to incentivize both winning and efficiency

## 🎓 Learning Outcomes

1. **Probabilistic Modeling:** Understanding HMMs and their applications
2. **Reinforcement Learning:** Q-learning, reward engineering, exploration strategies
3. **Hybrid Systems:** Combining different AI techniques effectively
4. **Evaluation Design:** Designing metrics that capture multiple objectives

## 📝 Future Improvements

If given more time:
1. **Deep Q-Network (DQN):** Handle more complex state representations
2. **Better State Encoding:** Include letter co-occurrence patterns
3. **Transfer Learning:** Pre-train on multiple corpora
4. **Dynamic Exploration:** Adaptive ε based on game state
5. **Ensemble Methods:** Combine multiple HMMs (by word length, frequency, etc.)
6. **MCTS Integration:** Monte Carlo Tree Search for look-ahead planning

## 📦 Dependencies
- Python 3.8+
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- tqdm
- Jupyter Notebook

## 👥 Author
Created for UE23CS352A: Machine Learning Hackathon

## 📄 License
Educational project - Department of Computer Science Engineering
