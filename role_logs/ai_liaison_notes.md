# AI Liaison Notes

## Assignment AI-use requirements

- The team must choose exactly one chat-based AI tool for the whole lab and any post-lab work. There should be no undocumented side conversations with other AI tools.
- Agentic AI tools may only be used as chat-based assistants. They must not directly produce the final submission without team review.
- AI-powered inline code completion is not permitted. Ordinary deterministic identifier completion, such as IntelliSense showing in-scope functions or variables, is permitted.
- The team must evaluate AI output critically because it may be wrong, incomplete, overcomplicated, outdated, or incompatible with the lab package rules.
- The final submission must include one verbatim AI interaction log, saved as `ai_log.md`, `ai_log.txt`, or `ai_log.pdf`. The log should include every prompt and every response, including any continuation between the in-person lab and submission deadline.
- The AI log is not the reflection. The QMD reflection should summarize how AI was useful or unhelpful, while the AI log should stay verbatim and unedited.
- If the selected AI tool has an outage, the team must inform the instructor and record any approved tool change in the QMD.
- The final QMD must include a brief AI-use reflection stating the tool used, one useful AI suggestion, one wrong/incomplete/overcomplicated/outdated/policy-incompatible AI response, and how the team identified and corrected the issue.
- The final QMD should also include the Verifier task results and each member's role and contribution.

## Draft AI-use reflection for QMD

Our team used `[insert exact chosen chat-based AI tool name]` as the single AI assistant for this lab. We used it to clarify the assignment requirements, plan ggplot2 approaches, and check whether our explanations matched the requested penguin bill-length and bill-depth comparisons. A useful AI suggestion was to connect the grouped bill-depth-versus-bill-length scatter plot to Simpson's paradox: the pooled trend can hide species-specific patterns, so we should compare the overall regression line with separate trend lines for each species instead of relying only on the ungrouped plot.

One AI response needed correction because it could give stronger conclusions than our own plots and verifier calculations supported. In particular, any claim that a trend was "statistically significant" or that species were "clearly separated" had to be checked against our rendered plots and our summary calculations, such as species-level means and correlations. We corrected this by using our own R output and verifier checks before writing the final interpretation. Since this workflow used AI subagents at the user's request, the final QMD text, code, plots, and interpretation should be reviewed by the human team before submission, and all AI interactions must be included verbatim in the AI log.

## Recommended points to mention

Useful AI suggestion:

- AI helped identify that the grouped scatter plot should be interpreted as a Simpson's paradox example, where the pooled relationship can differ from the species-specific relationships.

Questionable, incorrect, or incomplete AI issue:

- AI may make interpretation claims before seeing the team's exact rendered plots or computed verifier outputs. The team should mention that these claims were treated as drafts only and checked against the actual R results before being accepted.

Alternative policy-related issue to mention if it appears in the verbatim log:

- If any AI response suggested using `plotly`, base R plotting, or an extra package without justification, that should be recorded as a policy-incompatible suggestion. The correction is to use `ggplot2`, tidyverse packages, and `ggbeeswarm` only, unless the QMD gives the required one-sentence justification for another package.

## Final AI Liaison checklist

- Confirm the exact AI tool name used by the team.
- Confirm the QMD reflection matches the actual prompts and responses in the verbatim AI log.
- Confirm no undocumented AI side conversations are missing from the log.
- Confirm the human team reviewed and approved the final QMD wording before submission.
