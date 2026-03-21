# Strategy Research and Development Case

This case shows how I took a manual trading strategy and worked to automate it into a system that could trade independently.

## Goal
To turn a manual trading strategy into an algorithmic trading system suitable for live trading.

## Terminology
This case uses several Price Action concepts and abbreviated candlestick timeframe terms:

- **FVG (Fair Value Gap)** - a support/resistance zone in Price Action
- **Order Block (OB)** - a candlestick pattern in Price Action used as confirmation of a support/resistance zone
- **4H** - 4-hour candlestick timeframe
- **1H** - 1-hour candlestick timeframe

## Initial Strategy
The initial strategy was based on the following setup:

**Newest 4H FVG + 1H Order Block**

The strategy identifies the newest support or resistance zone, then looks for the first retest of that zone together with the appearance of confirmation.

From this baseline idea, various conditions and filters were applied to identify the conditions under which the strategy could be more predictable and suitable for live trading.

This strategy was developed and tested using EURUSD data.

Below is an example trade:

<table>
  <tr>
    <td align="center">
      <img src="images/strategy-research-and-development-case/sample-4h-FVG.png" alt="4H FVG example" width="420" /><br/>
      <sub><b>4H FVG</b></sub>
    </td>
    <td align="center">
      <img src="images/strategy-research-and-development-case/sample-1h-OB.png" alt="1H Order Block example" width="420" /><br/>
      <sub><b>1H Order Block</b></sub>
    </td>
  </tr>
</table>



## Manual Validation and Hand Labels
I integrated the strategy into my research infrastructure, which automatically captured chart screenshots for every detected setup. These screenshots were then reviewed manually to validate setup quality and assign a label.

Hand labeling was the most important step in this research process.

It acted as an early decision filter: if I could not consistently detect higher-quality setups from weaker ones before entry from a trader’s perspective, then the idea was not worth developing further.

This was a critical checkpoint, because it could save months of work that would otherwise be spent refining an idea with no real predictive structure.

Each setup was manually labeled as **Valid Entry**, **No Entry**, or **Unclear**.

This process helped me understand where the strategy actually worked, where it failed, and whether the setup showed enough consistency to justify deeper quantitative research.


Examples below show 1H chart structures used during manual validation. To improve dataset coverage, my research infrastructure can transform short setups into equivalent long-format examples. Since the setup is direction-neutral in EURUSD, this transformation was suitable and allowed me to increase the effective sample size.
<table>
  <tr>
    <td align="center">
      <img src="images/strategy-research-and-development-case/example-1.png" width="420"><br>
      <em>Figure 1. Clean retest with confirmation.</em><br>
      <strong>Label: Valid Entry</strong>
    </td>
    <td align="center">
      <img src="images/strategy-research-and-development-case/example-2.png" width="420"><br>
      <em>Figure 2. Extremum no longer valid.</em><br>
      <strong>Label: No Entry</strong>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="images/strategy-research-and-development-case/example-3.png" width="420"><br>
      <em>Figure 3. Confirmation structure is unclear.</em><br>
      <strong>Label: Unclear</strong>
    </td>
    <td align="center">
      <img src="images/strategy-research-and-development-case/example-4.png" width="420"><br>
      <em>Figure 4. Valid retest at the London session open.</em><br>
      <strong>Label: Valid Entry</strong>
    </td>
  </tr>
</table>

- visual review of setups
- image collection / trade examples
- manual labeling process
- labeled sample size
- year coverage
- match rate / validation outcome

## Why the Idea Was Worth Developing
- manual review showed that the setup had recognizable structure
- results were not random from a discretionary point of view
- this justified moving from visual pattern recognition to formal rule design

## Observation
Market behavior differs across trading sessions.

To reduce noise and build a more stable trading system, it makes sense to apply additional conditions. One of the key observations was that an Order Block formed during the **London open** or **New York open** may carry greater significance.

These periods are typically associated with higher volatility and stronger market participation. As a result, when confirmation appears during these sessions, the setup may have a higher probability of success.

Another important observation was related to trade exits. For better stability and predictability, it is preferable to use a clear and static target rather than a discretionary one.

In this strategy, a suitable target is the **high extremum of the support zone** for long trades, and the **low extremum of the resistance zone** for short trades. In other words, once the newest zone is identified and then successfully retested, the corresponding extremum of that zone can be used as the trade target.

## Baseline Performance

## Trade-Level Feature Infrastructure
- CSV per trade
- structured features
- analysis-ready dataset

## Filter 1: Trouble Area Before Target

## Filter 2: RR to Extremum

## Result: Higher Win Rate, but Weak Expectancy

## Next Research Direction: Improving Expectancy
- limit entries
- alternative execution logic

## Additional Research Branches
- second Order Block entry
- first-touch Order Block entry

## Key Takeaways
