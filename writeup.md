Marketing Mix Modeling with Mediation
1. Data Preparation

Dataset: 2 years of weekly data with revenue, media spends, email/SMS, price, promotions.

Transformations:

Log-transformed revenue (revenue_log) and Google spend (google_pred_log) to stabilize variance and allow elasticity interpretation.

Created binary “active” flags for weeks with zero spend.

Time trend index and Fourier seasonality terms (period=52 weeks) to capture weekly seasonality and long-term growth.

Feature engineering:

Applied adstock transformations to model carryover effects of media.

Controlled for average price and promotions.

2. Modeling Approach

Stage 1: Modeled Google spend (log) as a function of social media spends (Facebook, Instagram, TikTok, Snapchat) using Ridge regression with time-series CV.

Stage 2: Modeled log-revenue as a function of predicted Google spend, direct marketing levers (email/SMS), average price, promotions, and selected direct social channels using ElasticNet regression.

Hyperparameters: Ridge and ElasticNet regularization parameters tuned via cross-validation.

Validation: Used TimeSeriesSplit (no lookahead) and an expanding-window rolling CV to evaluate stability over time.

3. Causal Framing

Treated Google as a mediator between social spends and revenue.

Two-stage approach:

Estimate social → Google (stimulated search intent).

Estimate Google → Revenue while controlling for other levers.

Computed direct vs indirect effects of social channels:

Direct effect = coefficient in Stage 2.

Indirect effect = (social → Google coefficient) × (Google → Revenue coefficient).

This design prevents leakage and aligns with the assumed causal DAG.

4. Diagnostics

Performance:

Out-of-sample RMSE and MAPE showed reasonable predictive accuracy on holdout weeks.

Residuals: No major trends left unexplained, though mild autocorrelation exists.

Rolling CV: Coefficients and RMSE stable across different time windows, confirming robustness.

Sensitivity tests:

+5% average price → decrease in predicted revenue.

Promotions ON vs OFF → clear positive revenue lift.

5. Insights & Recommendations

Key drivers of revenue:

Google spend is the strongest driver, confirming mediation.

Price elasticity: Revenue decreases as average price rises.

Promotions: Clear positive lift.

Social channels:

Snapchat & Instagram: Positive indirect effect via Google.

TikTok: Small positive indirect effect, negligible direct effect.

Facebook: Small positive direct effect but large negative mediated effect (likely collinearity or substitution).

Risks:

Multicollinearity between social channels may distort individual coefficients.

Mediated effects sensitive to assumptions about Google’s role.

📌 Conclusion

This model provides a causal and interpretable view of marketing ROI.
Recommendations:

Prioritize Snapchat and Instagram for stimulating search demand.

Monitor Facebook campaigns closely due to potential inefficiencies.

Continue leveraging promotions strategically, but balance against long-term price sensitivity.

Treat estimates as directional rather than exact due to collinearity and mediation complexity.