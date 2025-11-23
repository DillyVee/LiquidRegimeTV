# FA-HMM Regime Detection Optimization Guide

## Overview
This guide explains how to optimize the FA-HMM regime detection strategy to find the best parameters for your market and timeframe.

---

## Quick Start - Use Presets

The easiest way to start is using the built-in presets:

### 1. **Conservative** (Lower Risk)
- Longer lookback periods (more stable)
- Higher confidence thresholds (fewer trades)
- More regime persistence (less switching)
- **Best for:** Volatile markets, longer timeframes (4H+)

### 2. **Moderate** (Balanced)
- Default parameters
- Balanced risk/reward
- **Best for:** Most markets, 1H-4H timeframes

### 3. **Aggressive** (Higher Frequency)
- Shorter lookback periods (more responsive)
- Lower confidence thresholds (more trades)
- Less regime persistence (faster switching)
- **Best for:** Trending markets, shorter timeframes (15m-1H)

**How to use:** In TradingView, set `Parameter Preset` to your choice.

---

## Adaptive Parameter Tuning

Enable `Enable Adaptive Parameters` to automatically adjust based on market conditions:

- **Trending Markets:** Increases CUSUM threshold (reduces false regime changes)
- **Volatile Markets:** Decreases CUSUM threshold (faster regime detection), reduces min duration
- **Ranging Markets:** Increases min regime duration (prevents whipsaws)

---

## Manual Optimization Using TradingView

### Step 1: Access Strategy Tester
1. Add the strategy to your TradingView chart
2. Open "Strategy Tester" panel at bottom
3. Click "Settings" gear icon

### Step 2: Set Optimization Parameters

Navigate to "Optimization" tab and configure:

#### Key Parameters to Optimize

| Parameter | Suggested Range | Step Size | Impact |
|-----------|----------------|-----------|---------|
| **Vol Fast Period** | 5-20 | 5 | Responsiveness to vol changes |
| **Vol Med Period** | 10-40 | 10 | Medium-term vol assessment |
| **Vol Slow Period** | 30-100 | 20 | Long-term vol baseline |
| **CUSUM Threshold** | 2.0-4.0 | 0.5 | Change-point sensitivity |
| **Min Regime Duration** | 3-15 | 3 | Regime stability |
| **Confidence Threshold** | 0.55-0.75 | 0.05 | Entry filter strictness |
| **Stability Threshold** | 0.50-0.70 | 0.05 | Entry filter strictness |
| **Max Leverage** | 1.0-2.5 | 0.25 | Position sizing aggression |

### Step 3: Choose Optimization Metric

Select the metric to optimize (in order of recommendation):

1. **Sharpe Ratio** ⭐ (Best for risk-adjusted returns)
2. **Profit Factor** (Best for overall profitability)
3. **Max Drawdown** (Best for capital preservation)
4. **Win Rate** (Best for psychological comfort)

### Step 4: Run Optimization

1. Click "Start Optimization"
2. TradingView will test all parameter combinations
3. Review results sorted by your chosen metric
4. Select the best parameter set

### Step 5: Validate Results

⚠️ **Critical:** Avoid overfitting!

1. **In-Sample Testing:** Use 70% of your data
2. **Out-of-Sample Testing:** Test on remaining 30%
3. **Walk-Forward Analysis:** Re-optimize every 3-6 months

---

## Advanced Optimization Strategy

### Multi-Timeframe Optimization

Test the same parameters across different timeframes:

| Timeframe | Recommended Preset | Key Focus |
|-----------|-------------------|-----------|
| **15m-1H** | Aggressive | Fast vol detection, low CUSUM |
| **1H-4H** | Moderate | Balanced parameters |
| **4H-Daily** | Conservative | Stable regimes, high confidence |

### Market-Specific Optimization

Different markets require different settings:

#### **Crypto Markets** (High Volatility)
```
Vol Thresholds: Lower (0.08, 0.20, 0.40)
CUSUM Threshold: Lower (2.5)
Min Duration: Lower (3 bars)
Confidence Threshold: Higher (0.70)
```

#### **Forex Markets** (Medium Volatility)
```
Vol Thresholds: Medium (0.10, 0.25, 0.50)
CUSUM Threshold: Medium (3.0)
Min Duration: Medium (5 bars)
Confidence Threshold: Medium (0.65)
```

#### **Stock Indices** (Lower Volatility)
```
Vol Thresholds: Higher (0.12, 0.30, 0.60)
CUSUM Threshold: Higher (3.5)
Min Duration: Higher (10 bars)
Confidence Threshold: Medium (0.65)
```

---

## Parameter Interaction Guide

Understanding how parameters work together:

### 1. **Regime Stability vs Responsiveness**

**More Stable (Fewer Regime Changes):**
- ↑ Increase `Min Regime Duration`
- ↑ Increase `Transition Smoothing`
- ↑ Increase `CUSUM Threshold`

**More Responsive (Faster Regime Detection):**
- ↓ Decrease `Min Regime Duration`
- ↓ Decrease `Transition Smoothing`
- ↓ Decrease `CUSUM Threshold`

### 2. **Trade Frequency**

**More Trades:**
- ↓ Lower `Confidence Threshold`
- ↓ Lower `Stability Threshold`
- ↓ Shorter vol lookback periods

**Fewer Trades (Higher Quality):**
- ↑ Higher `Confidence Threshold`
- ↑ Higher `Stability Threshold`
- ↑ Longer vol lookback periods

### 3. **Volatility Sensitivity**

**More Sensitive to Vol Changes:**
- ↓ Shorter `Vol Fast Period`
- ↓ Lower `Vol Thresholds`

**Less Sensitive (Smoother):**
- ↑ Longer `Vol Fast Period`
- ↑ Higher `Vol Thresholds`

---

## Optimization Workflow (Recommended)

### Phase 1: Baseline Testing (Week 1)
1. Test all 3 presets (Conservative, Moderate, Aggressive)
2. Run each for 1 month of data
3. Compare Sharpe Ratio and Max Drawdown
4. Choose best preset as baseline

### Phase 2: Coarse Optimization (Week 2)
1. Use wide parameter ranges
2. Large step sizes
3. Focus on top 3-5 parameters
4. Identify optimal region

### Phase 3: Fine-Tuning (Week 3)
1. Narrow parameter ranges around optimal region
2. Smaller step sizes
3. Test all optimizable parameters
4. Select best combination

### Phase 4: Validation (Week 4)
1. Out-of-sample testing
2. Different market conditions
3. Stress testing (crisis periods)
4. Forward testing (paper trading)

### Phase 5: Deployment
1. Deploy with best parameters
2. Monitor performance weekly
3. Re-optimize quarterly
4. Adjust for regime shifts

---

## Performance Metrics to Track

The strategy displays these optimization-relevant metrics:

### 1. **Regime Accuracy**
- % of regime calls that were correct
- Target: >60% for good performance
- <50% suggests poor parameters

### 2. **Total Regime Changes**
- Number of regime transitions
- Too many: Decrease sensitivity
- Too few: Increase sensitivity

### 3. **Net Profit**
- Overall strategy performance
- Use with Sharpe Ratio

### 4. **Confidence & Stability**
- Average levels over time
- Higher = better signal quality

---

## Common Optimization Mistakes

### ❌ **Overfitting**
- Testing too many parameters
- Optimizing on small datasets
- Not validating out-of-sample

**Solution:** Use walk-forward analysis, test on multiple time periods

### ❌ **Curve Fitting**
- Optimizing to past market conditions
- Ignoring regime changes

**Solution:** Test across different market regimes (bull, bear, crisis)

### ❌ **Ignoring Transaction Costs**
- Optimizing for max trades without considering slippage
- Not accounting for commissions

**Solution:** Include realistic commission (0.1%) and slippage (2 ticks)

### ❌ **Parameter Instability**
- Using parameters that work only in specific conditions
- No periodic re-optimization

**Solution:** Test parameter robustness, re-optimize quarterly

---

## Optimization Checklist

Before deploying optimized parameters:

- [ ] Tested on minimum 6 months of data
- [ ] Out-of-sample validation shows similar results
- [ ] Sharpe Ratio > 1.5
- [ ] Max Drawdown < 20%
- [ ] Regime Accuracy > 60%
- [ ] Profit Factor > 1.5
- [ ] Win Rate > 50%
- [ ] Tested across different market conditions
- [ ] Parameter values are reasonable (not extreme)
- [ ] Performance stable across different timeframes

---

## Quick Optimization Presets

### For Day Trading (15m-1H)
```
Vol Fast: 5
Vol Med: 15
Vol Slow: 40
CUSUM Threshold: 2.5
Min Duration: 3
Confidence: 0.60
```

### For Swing Trading (4H-Daily)
```
Vol Fast: 10
Vol Med: 30
Vol Slow: 80
CUSUM Threshold: 3.5
Min Duration: 8
Confidence: 0.70
```

### For Position Trading (Daily-Weekly)
```
Vol Fast: 15
Vol Med: 40
Vol Slow: 100
CUSUM Threshold: 4.0
Min Duration: 12
Confidence: 0.75
```

---

## Support & Further Reading

- **TradingView Optimization Docs:** https://www.tradingview.com/support/solutions/43000481029
- **Walk-Forward Analysis:** https://www.tradingview.com/support/solutions/43000681733
- **Strategy Testing Best Practices:** https://www.tradingview.com/support/solutions/43000481028

---

## Summary

1. **Start Simple:** Use presets first
2. **Enable Adaptive:** Let the system adjust automatically
3. **Optimize Gradually:** Don't change too many parameters at once
4. **Validate Results:** Always test out-of-sample
5. **Monitor & Adjust:** Re-optimize quarterly

The goal is finding **robust** parameters that work across different market conditions, not perfect parameters for historical data.
