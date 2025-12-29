Yield Curve
    ↓
Bond Pricing
    ↓
Portfolio Pricing
    ↓
DV01 & Scenario Analysis
    ↓
Historical Shock Estimation
    ↓
Monte Carlo PnL Distribution


# 1. Pulled Treasury par yields 
from FRED: DGS1MO, DGS3MO, DGS6MO, DGS1, DGS2, DGS5, DGS10, DGS30
# 2. Built a discount curve
Converted par yields → discount factors treating each tenor as a zero rate
# 3. Set Price bonds / portfolio
Defined each Treasury as: maturity (years), coupon rate, notional, and yield (interpolated from curve).
Priced with standard PV of cashflows (semiannual coupons).
# 4a. Compute DV01
Bumped discount curve +1bp, reprice, DV01 = -(P_bumped - P)/0.0001
# 4b. Simulate scenario shifts
Implemented stylized yield-curve scenarios. Simulated steepeners and flatteners to capture non-parallel curve risk

parallel: +X bp everywhere

steepener: short end down, long end up (or vice versa)

flattener: short up, long down

# 5. Historical Monte Carlo rate shocks
Used historical daily changes in curve nodes to estimate covariance.
Simulate correlated shocks, apply to nodes, reprice portfolio → return distribution and tail risk.

# Output (12/29/2025): 

As-of date: 2025-12-22
Portfolio price: 3,053,174.84
Portfolio DV01 (per 1bp): 1,495.40
Parallel +/−25bp scenario P&L: -37,076.09
Steepener +/−25bp scenario P&L: 20,349.09
Flattener +/−25bp scenario P&L: -20,199.70

Monte Carlo (1-day) portfolio P&L distribution:
{'base_price': 3053174.835114818, 'pnl_mean': -171.87795690525152, 'pnl_p01': -19471.557679889724, 'pnl_p05': -13937.528583089845, 'pnl_p50': -118.91777326725423, 'pnl_p95': 13473.412052119498}

