1. Evidence Mode Controls
  (evidence_mode) Flag
 
 The summarizer must support:
    - evidence_mode: "strict" | "normal"

  Strict Evidence Behavior (evidence_mode = "strict")
  - When strict mode is enabled:
    1. The summarizer may only use claims, facts, equations, and results explicitly present in the provided text.
    2. No external knowledge or assumptions may be added.
    3. If the summarizer cannot produce a meaningful summary using only the provided text, it must output:
      - “The source text does not provide enough detail to summarize this section in strict evidence mode.”
    4. No fabrication of methods, findings, concepts, or interpretations.

2. Section Warning Messages
  A. Empty Section
    - If the section has no content:
      - “Section content is invalid.”
    - The summarizer must skip summarization for that section.

  B. Short Section (< 50 words)
    - If the section contains fewer than 50 words:
      - “Insufficient content.”
    - The summarizer must still attempt a summary unless strict evidence mode prevents it.

  C. Excessive Input Length (Context Limit)
    - If the full input exceeds the system’s processing capacity:
      - “Input exceeds processing limits. Please divide the content into smaller chunks and resubmit.”
    - The summarizer must stop entirely.

3. Section Processing Logic
  - For every section, apply the following in order:
    1. Check for empty content
      - If empty → output:
        - “Section content is invalid.”
        - Skip summarization.

    2. Check for short content (< 50 words)
      - If short → prepend:
        - “Insufficient content.”

    3. Generate summary according to evidence mode:
      - Strict mode:
        - Use only information explicitly present.
        - If insufficient → output strict fallback message.
      - Normal mode:
        - Use full summarization capabilities.

    4. Output warnings (if any) followed by the summary.

4. Output Structure Requirements
  - When warnings apply, they must appear before the summary.
    - Example (short section):
      - Insufficient content. This section describes…
    - Example (short section + strict fallback):
      - Insufficient content. The source text does not provide enough detail to summarize this section in strict evidence mode.

5. Global Fail Condition — Context Limit
  - Before processing any sections:
    - If the entire input exceeds the system’s maximum context window, output only:
      - “Input exceeds processing limits. Please divide the content into smaller chunks and resubmit.”
    - Do not process any sections.

