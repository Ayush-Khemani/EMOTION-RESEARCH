# Emotion-Aware Chatbot Experiment: Loss Of Family Memeber

**Experiment Date:** 2025-11-12 

# Expriment Details:
User is processing the death of a close family member (parent). Journey through shock, denial, sadness, anger, guilt, and eventual acceptance over the conversation.

## Executive Summary

This experiment evaluates three approaches to integrating emotion detection into LLM responses across a 26-turn conversation in the **Loss Of Family Memeber** scenario.

### Quick Stats
- **Total Turns**: 26
- **Total API Cost**: $0.024696
- **Total Tokens Used**: 141211
- **HF-IBM Agreement Rate**: 53.8%
- **Average Emotion Confidence**: 0.770

---

## 1. Experimental Design

### Three Testing Modes

| Mode | Description |
|------|-------------|
| **1️⃣ Label Only** | Single emotion label passed to LLM |
| **2️⃣ Full Vector** | Complete emotion scores (all 6 emotions) passed to LLM |
| **3️⃣ Self-Detect** | LLM detects emotion from text without external input |

### Emotion Detection Pipeline
- **Hugging Face**: `bhadresh-savani/bert-base-uncased-emotion`
- **IBM Watson**: Natural Language Understanding v2021-08-01
- **Merge Strategy**: 60% HF + 40% IBM Watson weighted average

---

## 2. Results Overview

### Emotion Distribution

- **SADNESS**: 36 turns (46.2%)
- **JOY**: 27 turns (34.6%)
- **FEAR**: 9 turns (11.5%)
- **ANGER**: 6 turns (7.7%)

### Mode Performance Comparison

| Mode | Turns | Avg Confidence | Total Tokens | Total Cost |
|------|-------|----------------|--------------|-----------|
| 1️⃣ | 26 | 0.770 | 43899 | $0.007660 |
| 2️⃣ | 26 | 0.770 | 56542 | $0.009938 |
| 3️⃣ | 26 | 0.770 | 40770 | $0.007098 |


### HF-IBM Model Agreement
- **Agreement Cases**: 42 out of 78
- **Agreement Rate**: 53.8%
- **Disagreement Rate**: 46.2%

---

## 3. LLM Response Quality Analysis

### Sentiment & Empathy Metrics by Mode


**1️⃣:**
- Avg Sentiment Words: 0.65
- Avg Empathy Indicators: 2.46
- Emotional Tone Intensity: 60.51

**2️⃣:**
- Avg Sentiment Words: 1.19
- Avg Empathy Indicators: 2.42
- Emotional Tone Intensity: 81.69

**3️⃣:**
- Avg Sentiment Words: 0.46
- Avg Empathy Indicators: 1.88
- Emotional Tone Intensity: 56.64


### Correlation Analysis
Higher emotion confidence correlates with:
- Sentiment Words: 0.339
- Empathy Indicators: -0.065
- Response Length: 0.086

---

## 4. Key Findings

### Emotion Detection
1. HF and IBM show 53.8% agreement rate
2. Most detected emotion: **SADNESS** (36 turns)
3. Average emotion confidence: 0.770 (high confidence)

### LLM Response Behavior
1. Mode 1 (Label Only) - nan sentiment words on average
2. Mode 2 (Full Vector) - 1.19 sentiment words on average
3. Mode 3 (Self-Detect) - 0.46 sentiment words on average

---

## 5. Files Generated

### Data Files
- `conversation_log_Mode1_LabelOnly.csv` - Mode 1 conversation data
- `conversation_log_Mode2_FullVector.csv` - Mode 2 conversation data
- `conversation_log_Mode3_SelfDetect.csv` - Mode 3 conversation data
- `merged_analysis.csv` - Combined data from all modes
- `detailed_analysis.csv` - Detailed emotion scores and metrics
- `statistics.json` - Summary statistics

### Visualizations (20 PNG images)

**Emotion Detection Analysis (1-10):**
1. Emotion Distribution Across Modes
2. Emotion Score Heatmap by Mode
3. Confidence Distribution
4. HF vs IBM Model Comparison
5. HF-IBM Agreement Rate
6. Emotion Progression Over Turns
7. Token Usage by Mode
8. Cost Analysis by Mode
9. Response Length Distribution
10. Total Emotion Counts

**LLM Impact Analysis (11-20):**
11. Sentiment Words by Mode
12. Empathy Indicators by Mode
13. Emotional Tone Intensity by Mode
14. Emotion Confidence vs Sentiment Words
15. Emotion Confidence vs Empathy
16. Correlation Heatmap
17. Response Length by Mode & Emotion
18. Mode Impact Comparison
19. HF Emotion Impact on Response
20. IBM Emotion Impact on Response

---

## 6. Technical Details

### Models & APIs
- **HuggingFace Model**: bhadresh-savani/bert-base-uncased-emotion
- **IBM Watson NLU**: v2021-08-01
- **LLM**: OpenAI GPT-4o-mini

### Cost Breakdown
- **Mode 1 Total**: $0.000000
- **Mode 2 Total**: $0.009938
- **Mode 3 Total**: $0.007098
- **Total Experiment Cost**: $0.024696

### Token Usage
- **Mode 1 Total**: 0 tokens
- **Mode 2 Total**: 56542 tokens
- **Mode 3 Total**: 40770 tokens
- **Total Tokens**: 141211 tokens

---

## 7. Conclusion

This experiment demonstrates how different approaches to emotion integration affect LLM response generation. The detailed visualizations and metrics provide insights into:

✅ How well external emotion detection models (HF + IBM) agree  
✅ Which mode produces more emotionally aware responses  
✅ The correlation between emotion confidence and response quality  
✅ The impact of emotion input on LLM behavior across different scenarios  

---

## 8. How to Use This Data

1. **View Visualizations**: Open the `visualizations/` folder to see all 20 PNG charts
2. **Analyze CSV Data**: Import CSVs into Excel, Pandas, or your analytics tool
3. **Read Statistics**: Check `statistics.json` for key metrics
4. **Compare Modes**: Use detailed_analysis.csv to compare mode performance

---