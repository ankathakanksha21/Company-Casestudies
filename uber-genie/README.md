# Uber Genie: 5 engineering lessons from building a RAG assistant

Uber built Genie, an internal RAG assistant that answers engineering questions in Slack.

## First-year numbers

| Metric | Value |
| --- | --- |
| Questions answered | 70,000+ |
| Slack channels | 154 |
| Answers rated helpful by users | ~49% |
| Engineering hours saved (estimated) | 13,000 |

## 1. Put the assistant where people already ask questions

Engineers already ask for help in Slack support channels, so Genie answers there automatically. There's no new tool to adopt, which is why people actually use it.

## 2. Keep the knowledge fresh

Uber's answers were spread across multiple sources that kept changing:

- Internal wiki
- Internal Stack Overflow
- Slack
- Other docs

A daily pipeline re-indexes every source and keeps Genie's answers current. Refresh your data on a schedule, or your assistant will give out-of-date answers.

## 3. Find the right chunk

A raw chunk of text often doesn't match how people word their questions, so search misses it. Before indexing, an LLM adds three things to each chunk:

- A short summary
- Keywords
- Likely FAQs

This gives search more ways to match a question to the right chunk.

## 4. Reduce hallucinations

- **Cite every answer.** Each retrieved chunk goes into the prompt labelled with its source URL, and the model has to cite those URLs.
- **Proper handoff.** When the docs don't cover a question, Genie points the user to the on-call team instead of guessing.

## 5. Measure quality and cost

- **Collect feedback you can act on.** Genie uses four buttons instead of a thumbs up or down: Resolved, Helpful, Not Helpful and Not Relevant. This tells you exactly what went wrong.
- **Grade the answers and the docs.** An LLM judge scores Genie's answers against golden answers that experts wrote once. The judge also grades the source docs and suggests fixes to them, because better docs mean better answers.
- **Track cost per request.** A request ID travels through every call, from Slack to the LLM, so you can trace the cost of every question.
