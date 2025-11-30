1. Iterate through each provided text section in order.
  - Treat each section independently but maintain global length constraints.
2. Summary Level Mode (summary_level)
  The summarizer must support two output modes:

  A. summary_level = "short"
    - Output only a 1–2 sentence compact summary of the section.
    - Do not include bullet points.

  B. summary_level = "detailed"
    - Output a short paragraph summarizing the section.
    - Follow with a bullet list of 3–5 key points highlighting essential details.

  Conditional Behavior in Section Loop:
    - When processing each section:
      - If summary_level = "short" → generate ONLY the compact summary.
      - If summary_level = "detailed" → generate the paragraph + bullet list.

3. Focus Check (Key Topics Prioritization)
  - If the user provides Key Topics, prioritizes summarizing details related to those topics.
  - If a section is largely irrelevant to the Key Topics:
    - Summarize minimally (1 sentence if short mode, reduced paragraph/bullets if detailed mode).

4. Length Monitor
  - Continuously track total word count of the generated summary.
  - Ensure the final output does not exceed Maximum Summary Length.
  - If output approaches the limit:
    - Prefer compressing less-relevant sections.
    - Maintain coverage of high-priority or Key Topic–related content.
