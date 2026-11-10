# Hawky platform history

This document is a user-facing summary of documented Hawky platform release checkpoints and bug-fix work. It describes repair areas without exposing internal implementation details, runtime measurements, credentials, or service/provider names.

Entries are ordered newest first. Hawky platform versions and Android app versions are separate release tracks. Android app v1.0.0 was introduced alongside Hawky platform v2.6.0; Android version numbers are not platform version numbers. This history does not imply that every feature is enabled for every account or distribution channel.

## Hawky platform v2.7.0 update — November 2026

### Strategy and analysis intelligence

- Added a Performance Breakdown to Algorithm that groups closed Paper positions by signal source, pool type, exit reason and holding time, so the sources and exits that make or lose money are visible at a glance.
- Added Winning Settings to Algorithm: it compares the filter and exit settings of an account's best and worst recent strategies with the current configuration and marks each setting as matching the winners or sitting closer to the losers. It is advice only and never changes settings automatically.
- Introduced a self-calibrating entry score that runs alongside the existing Hawky score in observation mode. It retrains from closed Paper positions on a rolling window and only replaces its active calibration with one that performed better on positions it had not seen; if results regress, it searches for a better calibration on its own. It does not block or size entries.
- Added observation-mode regime guards in Algorithm: a performance pause after a losing streak and a self-calibrated trading-hours filter. Each Paper entry records what the guards would have done, so their value can be measured before either is allowed to act.
- Edge now provides an entry advisory for Hawky Local: every Local Paper entry shows a calibrated win probability and a Favorable / Neutral / Unfavorable verdict relative to the strategy's recent entries. In automatic mode the advisory earns influence step by step (observe, then reduced size, then skipping the weakest entries) only after closed positions prove it right, and steps back when newer results stop confirming it. Influence applies to Paper only.
- Improved Edge probability estimates and added a discrimination measure next to calibration, so it is clear whether Edge can actually tell stronger entries from weaker ones. Default Edge Paper exit settings were updated based on recorded position behavior.
- Added a Realized Risk panel to Risk Center with drawdown from the equity peak, losing streaks, average win versus average loss, tail loss, the real result of stop-loss exits compared with the configured stop, daily results, and a position-size guide.
- Filtered Signals now show each entry's return, exit type, holding time, advisory verdict and score, with a win-rate and net summary of the listed entries.
- Wallet Behavior Drift now includes a wallet value summary showing which followed wallets contributed the most and the least to Paper results. Nothing is unfollowed automatically.

### Entry safeguards

- The first-minute launch guard (anti-scam) now receives real launch evidence more often and rejects confirmed oversized launches earlier, before they reach the candidate list. When evidence is not available, the check never blocks an entry, and implausible values are ignored.
- On-chain structural checks no longer mark tokens from other launch venues as unknown when a source suggested a different venue.

### Website, mobile and public site

- Introduced a new public landing page with Paper-mode guidance, store badges and a compact mobile layout.
- Website Portfolio now shows the account's virtual Paper wallets, active-wallet status and closed-position results instead of an on-chain view.
- Unified card frames, typography and symmetry across Website, mobile, Android and iOS views, including the square summary cards, Watchlist alignment and header layout.
- Improved the desktop account toolbar and mobile layouts for Strategy Lab tables and dashboard cards.

### Reliability and performance

- Candidate scanning now continues immediately while eligible signals are waiting instead of pausing between cycles, so queued signals are analyzed sooner.
- Static token facts resolved by one workspace are now shared with the other workspaces for the lifetime of the signal, reducing repeated work in the shared analysis queue. Prices, liquidity, volume and every account decision remain specific to each workspace.
- Fixed Strategy Ranking staying in a pending state while trading was active.
- Fixed the low-score strategy cleanup so it applies to every eligible strategy profile, runs periodically and when the threshold changes, and always keeps the strategy that is currently trading.
- Corrected the Brain confirmed-entry counter, which counted each entry twice, and stopped position lifecycle events from inflating candidate statistics.
- Corrected stop-loss labels in Risk Center, research history retention and multi-timeframe research statistics, and Prefilter source switches that did not reflect their live state immediately.

## Hawky platform v2.7.0 — November 2026

### New and expanded capabilities

- Added an experimental Watchlist price-projection corridor for supported open Paper positions when the available history is sufficient. The projection can update as valid position data arrives, follows the configured holding horizon, and remains informational: it does not control entries, exits, or execution.
- Added configurable RSI entry bounds alongside the existing signal-analysis controls.
- Strengthened liquidity-related candidate safeguards and made security-review outcomes easier to identify.
- Expanded position review and sharing, including result cards based on the combined outcome of a closed Paper position.
- Expanded strategy and risk research with Strategy Lab, Strategy Library, Strategy Ranking, and Risk Center for accounts with access.
- Improved password setup and activation feedback, notification preferences, mobile position controls, navigation, and responsive layouts.
- Expanded Paper wallet management with virtual balances that track realized Paper results, per-wallet deletion, and preservation of recorded position history.
- Improved PNL and Sells history review with paginated closed-position results and performance summaries for the selected daily, weekly, or monthly period.

### Reliability and bug fixes
- Fixed history pagination and period-selection persistence across navigation and refreshes.
- Corrected issues in candidate intake, review status, and the handoff from signal analysis to position monitoring.
- Improved quote freshness and recovery, chart refresh behavior, and position updates during open and close transitions.
- Fixed account activation, session recovery, notification-state, and menu-loading issues.
- Corrected inconsistencies in position summaries, shared results, and mobile layouts.

## Android app v1.0.9 — November 2026, version code 13

- New risk protection filters in Entry Filters to help avoid high-risk tokens, including an optional advanced filter that is off by default.
- Faster analysis when many accounts are active, with shorter waiting times.
- Paper Portfolio for Website accounts now shows virtual wallets and closed-trade results.
- Algorithm adds new performance and risk insights, including best-settings comparisons and drawdown tracking.
- Stronger protection against suspicious new tokens.
- More reliable signal sources, with clearer status when a source has no data.
- Phone layout improvements across every menu: uniform cards, easier-to-read help text and cleaner navigation.
- Stability and accuracy fixes across trading statistics and the scanner.

This is an Android app milestone, separate from Hawky platform v2.7.0.

## Android app v1.0.7 — October 2026 test build, version code 11

- Grouped navigation into expandable sections and improved visual consistency and loading feedback.
- Refined position, session, and alert controls for mobile screens.
- Improved responsiveness when opening analysis tools.

This is an Android app milestone, separate from Hawky platform v2.7.0.

## Hawky platform v2.6.0 — October 2026

### Website accounts and signal tools

- Expanded Website account activation, account-specific Paper workspaces, menu permissions, and account data controls.
- Improved tracked-wallet signal summaries and follow-up review.
- Expanded research and strategy tools, including wallet performance, Strategy Lab, and account-level review surfaces.
- Improved account menu defaults and the consistency of account settings across sessions.

### Reliability and bug fixes

- Corrected account-isolation, account-cleanup, and account-lifecycle issues affecting Website workspaces.
- Fixed signal delivery and attribution problems, including inconsistencies in account-specific activity and Paper summaries.
- Corrected history counters, transaction and quote presentation, and refresh behavior.
- Fixed mobile navigation and execution-layout overlaps, along with post-close chart polling issues.
- Unified card typography, table alignment, and other interface details across Local and Website surfaces.

## Hawky platform v2.5.0 — October 2026

### Analysis and review

- Expanded Edge Paper evaluation and qualification workflows while keeping unqualified automation disabled by default.
- Improved activity and history review, source-quality summaries, and the responsiveness of analysis views.
- Added additional transaction context to tracked-wallet activity where available.

### Reliability and bug fixes

- Improved candidate and inbox handling, including bounded history views and more predictable processing under load.
- Corrected quote-waiting and position-evidence handling, and improved recovery during startup and replay.
- Reduced unnecessary work in history and analytics views to keep the active analysis and position-monitoring experience responsive.
- Clarified qualification states so an unqualified Paper strategy is not presented as ready for autonomous use.

## Hawky platform v2.4.0 — October 2026

### Signal and position workflow

- Improved signal delivery between Local and Website Paper workspaces while keeping each Website account's settings and position history separate.
- Strengthened coordination of candidate analysis and improved quote continuity for open positions.
- Refined Edge analysis and Paper review workflows.

### Reliability and bug fixes

- Fixed signal handoff and ordering issues affecting concurrent workers.
- Improved recovery from quote gaps and transitions between market states.
- Refined startup readiness and background warm-up so active workflows can resume more predictably.

## Hawky platform v2.3.0 — October 2026

### Website workspaces

- Introduced isolated Paper workspaces for Website accounts, with account-specific settings, activity, positions, and history.
- Added delivery of admitted signals to active Website workspaces, where each account applies its own configured analysis and Paper rules.
- Expanded account lifecycle, access controls, menu permissions, and account-level activity review.
- Improved Website Watchlist, position monitoring, realized-Paper summaries, and mobile navigation.

### Reliability and bug fixes

- Repaired Website worker startup and recovery paths, including cases where a worker failed to become ready or did not recover cleanly after a delayed response.
- Corrected account-specific quote continuity, closed-position summaries, counters, and chart behavior.
- Fixed account cleanup and Paper-history integrity issues.
- Improved sign-in protection, menu access consistency, and mobile navigation and layout.

## Hawky platform v2.2.0 — September 2026

### Candidate review and position controls

- Expanded Prefilter candidate review, queue visibility, and signal-status presentation.
- Improved the Watchlist for multiple open positions and refined real-time position and exit-trigger displays.
- Expanded configurable position targets and review of Paper exit plans.
- Improved candidate security and market-quality review.

### Reliability and bug fixes

- Corrected quote and snapshot consistency used during candidate decisions and position updates.
- Fixed trigger revalidation, position PNL receipts, and closed-position records to keep displayed outcomes aligned with accepted position data.
- Repaired chart handoffs between active and recently closed positions and improved post-close updates.
- Cleaned up invalid legacy records and corrected Paper history and deletion behavior.

## Hawky platform v2.1.0 — September 2026

### Candidate analysis and research

- Expanded Prefilter status review, candidate pagination, and security-analysis visibility.
- Improved Research outcome processing and compact performance summaries.
- Refined the Watchlist labels and presentation of position and candidate information.

### Reliability and bug fixes

- Improved handling of delayed security results so late information cannot silently change an already completed decision.
- Corrected rejected-candidate cleanup and Paper deletion consistency.
- Reduced unnecessary work in history, analytics, and summary views while preserving position monitoring and execution behavior.
- Improved candidate-processing responsiveness and recovery from temporary analysis delays.

## Hawky platform v2.0.0 — September 2026

### Major platform expansion

- Introduced the Prefilter signal-review workflow and its candidate-management interface.
- Added completed snapshot handoff into downstream candidate review.
- Expanded the Watchlist to display and regroup multiple open Paper positions.
- Expanded Edge analysis and position-risk review.

### Reliability and bug fixes

- Corrected quote integrity and market-state routing used by candidate and position workflows.
- Improved handling of stale, missing, and inconsistent position updates, including recovery after quote gaps.
- Fixed Paper PNL and risk-state presentation and strengthened safeguards around position closure.
- Improved chart layout and position grouping when the number of open positions changes.

## Hawky platform v1.0.1 — September 2026

- Improved Research outcome processing so older pending reviews continue to be handled during busy periods.
- Refined Algorithm, Brain, and Research views, including labels, help text, counters, and layout.
- Improved configuration clarity and persistence across the analysis interface.
- Continued targeted fixes to candidate review and the consistency of displayed analysis results.

## Hawky platform v1.0.0 — September 2026

- Established the first documented platform release checkpoint for Hawky's signal-to-position workflow.
- Added lifecycle review surfaces for following Paper activity and understanding candidate progression.
- Introduced a reference-strategy view for reviewing historical Paper outcomes.
- Improved the reliability of starting and restarting the platform workspace.

## Bug-fix work across releases

Across the documented releases, focused repair work covered these user-visible areas:

- **Signals and candidate decisions:** clearer status transitions, more reliable handoffs, improved rejection and follow-up visibility, and better handling of delayed or incomplete analysis.
- **Quotes and open positions:** fresher position updates, recovery from gaps, safer handling of market-state changes, and more consistent charts while positions open, change, and close.
- **Paper results and history:** more consistent PNL, counters, exit records, deletion, and account-specific history.
- **Website accounts:** account activation and session recovery, isolated account workspaces, access permissions, cleanup, and worker startup reliability.
- **Interface and mobile use:** responsive layouts, navigation, chart controls, readable tables, consistent typography, and more predictable loading and refresh behavior.
- **Analysis responsiveness:** reduced unnecessary work in historical and summary views so that active signal and position workflows remain responsive.

These are summaries of documented release checkpoints, not a claim that every individual internal patch is listed or that all features are enabled on every distribution track.

## Android app milestones — separate version track

- **Android app v1.0.9, version code 13:** update with new risk protection filters, faster analysis, Website Paper Portfolio and phone layout improvements.
- **Android app v1.0.7, version code 11:** test build with navigation, loading, and mobile-control refinements.
- **Android app v1.0.4:** early-access update focused on mobile layout, position exposure, session controls, and notification presentation.
- **Android app v1.0.1:** Solana Mobile dApp Store launch milestone.
- **Android app v1.0.0:** introduced alongside Hawky platform v2.6.0.

Android app versions do not identify Hawky desktop/Website platform releases. Availability and release status depend on the relevant distribution channel.
