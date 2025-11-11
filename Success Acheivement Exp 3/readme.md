# Emotion-Aware Chatbot Experiment: Achievement Success Scenario

## Executive Summary
This experiment evaluates three different approaches to integrating emotion detection into LLM responses. A user experiencing achievement success (job offer, exam score, project approval) with subsequent self-doubt engages in a 25-turn conversation tested across three modes using Hugging Face and IBM Watson emotion detection models.

---

## 1. Experiment Information

| Property | Value |
|----------|-------|
| **Scenario** | Achievement Success (Mixed Emotions) |
| **Date Conducted** | [11-11-2025] |
| **Total Turns** | 25 |
| **Modes Tested** | 3 |
| **Emotion Models** | Hugging Face BERT + IBM Watson NLU |
| **LLM Model** | OpenAI GPT-4o-mini |

---

## 2. Research Objective

**Main Question:** How do different approaches to emotion detection input affect LLM response quality?

**Sub-Questions:**
1. How well do HF and IBM agree on emotion detection?
2. Which mode (label only vs. full vector vs. self-detect) produces better responses?
3. How do emotion confidence scores vary across the conversation?
4. What is the emotional progression detected by both models?

---

## 3. Scenario Description

### Context
User shares achievement success (job offer, exam score, project approval) but develops mixed emotions including imposter syndrome, self-doubt, and anxiety about future performance.

### Emotional Journey
- **Turns 1-10**: Pure celebration and joy
- **Turns 11-20**: Transition to anxiety, self-doubt, and mixed emotions
- **Turns 21-25**: Self-reflection, acceptance, and resolution

### User Input
All 25 conversation turns were **manually crafted** by the researcher to create a realistic emotional arc.

---

## 4. Experimental Design

### Three Testing Modes

#### **Mode 1: Rule → LLM (Emotion Label Only)**
- Input to LLM: Single emotion label from merged HF+IBM detection
- Format: "The user's detected emotion is: [JOY/FEAR/SADNESS/etc.]"
- Purpose: Minimal context - only top emotion
- Expected Impact: Basic emotion awareness

#### **Mode 2: Array → LLM (Full Emotion Vector)**
- Input to LLM: All 6 emotion scores with confidence values
- Format: "Detected emotions: joy: 0.92, fear: 0.42, sadness: 0.15, anger: 0.08, disgust: 0.05, surprise: 0.22"
- Purpose: Rich emotional context - full emotional state
- Expected Impact: More nuanced, contextual responses

#### **Mode 3: LLM Only (No Rule-Based Input)**
- Input to LLM: No emotion detection input
- Format: "Detect the user's emotion from the text and reply accordingly"
- Purpose: Baseline - LLM self-detection only
- Expected Impact: Generic responses without explicit emotion guidance

---

## 5. Emotion Detection Pipeline

### Models Used

| Model | Purpose | Output |
|-------|---------|--------|
| **Hugging Face** | Emotion classification | 6 emotions (joy, sadness, anger, fear, disgust, surprise) with sigmoid scores |
| **IBM Watson** | Document emotion analysis | 6 emotions with confidence scores |
| **Merge Strategy** | Combine both models | Weighted average: 60% HF + 40% IBM Watson |

### Emotion Labels
- **Joy**: Happiness, excitement, satisfaction
- **Sadness**: Grief, disappointment, sorrow
- **Anger**: Frustration, irritation, rage
- **Fear**: Anxiety, worry, concern
- **Disgust**: Revulsion, contempt, disapproval
- **Surprise**: Amazement, shock, astonishment

---

## 6. Data Collection

### Metrics Tracked Per Turn

| Category | Metric | Details |
|----------|--------|---------|
| **Emotion Detection** | HF Label | Top emotion from Hugging Face |
| | IBM Label | Top emotion from IBM Watson |
| | Final Label | Merged emotion (60% HF + 40% IBM) |
| | HF Scores | All 6 emotion confidence scores |
| | IBM Scores | All 6 emotion confidence scores |
| | Merged Scores | All 6 merged confidence scores |
| **LLM Response** | Bot Reply | Full response text |
| | Tokens Used | Total tokens consumed |
| | Cost | USD cost of API call |
| | Response Length | Word count |
| **Test Context** | Mode | Which testing mode (1, 2, or 3) |
| | User Message | Original user input |

---

### 7. CSV Structure
Each CSV contains 25 rows (one per turn) with columns:
- `user`: User message
- `mode`: Test mode (1, 2, or 3)
- `hf_label`: HuggingFace detected emotion
- `ibm_label`: IBM Watson detected emotion
- `final_label`: Merged emotion
- `hf_scores`: HF confidence scores (dict)
- `ibm_scores`: IBM confidence scores (dict)
- `merged_scores`: Merged confidence scores (dict)
- `bot_reply`: LLM response
- `tokens_used`: Total tokens consumed
- `cost_usd`: Cost of API call
- `response_length`: Word count

---

## 8. Results Collected

### Emotion Detection Results

#### HF-IBM Agreement
- **Total Turns**: 75 (25 turns × 3 modes)
- **Agreement Rate**: 28.0% (21/75 turns)
- **Disagreement Rate**: 72.0% (54/75 turns)
- **Key Finding**: HF and IBM Watson show significant disagreement, suggesting they capture different aspects of emotion or have different sensitivities to emotional cues

#### Detected Emotion Distribution

| Emotion | Mode 1 Count | Mode 2 Count | Mode 3 Count |
|---------|-------------|-------------|-------------|
| Joy | 15 | 15 | 15 |
| Fear | 5 | 5 | 5 |
| Anger | 2 | 2 | 2 |
| Sadness | 3 | 3 | 3 |
| Disgust | 0 | 0 | 0 |
| Surprise | 0 | 0 | 0 |

**Key Finding:** Joy is the dominant detected emotion across all modes (60% of turns), which aligns with the scenario's achievement success theme.

#### HF-IBM Disagreement Patterns
Common disagreement patterns observed:
- **HF predicts Anger → IBM predicts Joy** (Turns 1-3): Likely due to exclamatory language ("literally screamed")
- **HF predicts Joy → IBM predicts Sadness** (Turns 4-9): IBM may be more sensitive to underlying self-doubt language
- **HF predicts Fear → IBM predicts Sadness** (Later turns): Different interpretation of anxiety expressions

---

## 9. Mode Comparison

### Response Characteristics by Mode

| Metric | Mode 1 (Label) | Mode 2 (Vector) | Mode 3 (Self-Detect) |
|--------|--------------|----------------|-------------------|
| **Unique Emotions Detected** | 4 | 4 | 4 |
| **Most Common Emotion** | Joy | Joy | Joy |
| **Avg Confidence** | 0.746 | 0.746 | 0.746 |
| **Confidence Std Dev** | 0.107 | 0.107 | 0.107 |
| **HF-IBM Agreement** | 28.0% | 28.0% | 28.0% |

**Key Finding:** All three modes produce identical emotion detection results, indicating that the 60% HF + 40% IBM weighting consistently produces the same final emotions regardless of the prompt format.

---

## 10. Key Observations

### Emotion Detection Insights

**1. Low HF-IBM Agreement (28.0%)**
- HF and IBM Watson disagreed on 72% of turns, suggesting they use different feature extraction methods
- This disagreement is important because it indicates model diversity - each captures different aspects of emotion
- The 60/40 weighted merge helps balance both perspectives

**2. Joy Dominance**
- 60% of all detected emotions were Joy (15/25 turns)
- This aligns with the scenario design where the first 10 turns celebrate achievements
- Even in turns 11-20 (mixed emotions), Joy remained the dominant label

**3. Limited Emotion Diversity**
- Only 4 unique emotions detected: Joy, Fear, Sadness, Anger
- Disgust and Surprise were not detected despite being present in the scenario design
- Suggests these models may have lower sensitivity to subtle emotional expressions

**4. Emotion Confidence Analysis**
- **Average Max Confidence:** 0.746 (Strong confidence)
- **Average Min Confidence:** 0.008 (Very low secondary emotions)
- **Confidence Range:** 0.738 (Large gap between top and secondary emotions)
- **Interpretation:** Models are highly confident in their primary emotion classification but show very low confidence in alternative emotions

**5. Model Consistency**
- All three modes produced identical emotion detection (since emotion detection happens before mode-specific prompting)
- The difference between modes lies in how this emotional information is presented to the LLM, not in the emotion detection itself

### LLM Response Patterns

The three modes differ in how they present emotion context to the LLM:

- **Mode 1 (Label Only):** Simple instruction like "emotion is: joy"
- **Mode 2 (Full Vector):** Detailed breakdown like "joy: 0.629, fear: 0.295, sadness: 0.332..."
- **Mode 3 (Self-Detect):** No explicit emotion guidance; LLM infers from text

However, all three modes received identical upstream emotion data from HF+IBM detection.

### Disagreement Pattern Analysis

Key cases where HF ≠ IBM:

1. **Exclamatory Joy (Turns 1-3)**
   - User: "I literally screamed when I opened the email!"
   - HF detects: Anger (exclamation intensity)
   - IBM detects: Joy (semantic understanding)
   - Shows HF may conflate strong emotion expression with anger

2. **Self-Doubt Expressions (Turns 11-15)**
   - User: "Part of me keeps waiting for something to go wrong"
   - HF detects: Joy (overall context)
   - IBM detects: Sadness (pessimism language)
   - Shows IBM more sensitive to negative sentiment phrases

3. **Mixed Emotions (Turns 21-25)**
   - User: "I'm both happy AND nervous"
   - Both models struggle with genuine mixed emotions
   - Resolution usually defaults to primary emotion (Joy)

### Model Comparison (HF vs IBM)

| Characteristic | Hugging Face | IBM Watson |
|---|---|---|
| **Sensitivity to exclamations** | High (may misclassify as anger) | Moderate (better semantic understanding) |
| **Handling of negation** | May miss sarcasm/negation | Better at semantic negation |
| **Mixed emotion support** | Limited | Limited |
| **Overall pattern** | More conservative, excitation-sensitive | More nuanced, semantics-driven |

---

## 11. Technical Details

### API Configuration
- **Hugging Face Model**: `bhadresh-savani/bert-base-uncased-emotion`
- **IBM Watson**: Natural Language Understanding v2021-08-01
- **OpenAI Model**: `gpt-4o-mini`
- **HF-IBM Weight Ratio**: 60% HF, 40% IBM Watson


