# TakeMeter Label Definitions

## Label 1: Sourced Information
**Label:** sourced_information

**Definition:** Posts that primarily report information attributed to an identifiable external source, such as a news article, research paper, official announcement, or cited report.

**Example posts:**
- “A new research paper evaluates how AI systems perform on complex reasoning tasks.”
- “According to a report published this week, several companies are expanding their use of AI tools.”


## Label 2: Personal Experience or Opinion
**Label:** personal_opinion

**Definition:** Posts that primarily express the author's personal experience, opinion, preference, reaction, or prediction about AI or technology.

**Example posts:**
- “I've tried several AI video generators, and this one is the easiest for me to use.”
- “I think AI coding assistants will become a standard part of software development.”
- “It's kind of hard to find a video generator that meets my needs.”


## Label 3: Unsupported Broad Claim
**Label:** unsupported_claim

**Definition:** Posts that primarily make a broad factual assertion about AI or technology without citing an identifiable source or providing specific supporting evidence. The claim may sound confident, but the post does not give enough evidence to establish it.

**Example posts:**
- “AI will replace every software developer within two years.”
- “Every company that adopts AI becomes more productive.”
- “AI systems are always more accurate than human experts.”

**Important distinction:** A post does not belong in this category merely because it discusses a broad topic or includes explanations, reasoning, or examples. If it provides specific evidence or attributes its information to a source, consider sourced_information. If its main purpose is to express a personal opinion or prediction, consider personal_opinion.

## Decision Rules

Apply these rules consistently when assigning one label to each post.

**Identify the post's primary purpose.** Determine whether it mainly reports externally attributed information, expresses the author's own perspective, or asserts a factual claim without adequate support.

**Choose sourced_information** when the post primarily reports information attributed to an identifiable external source. A link alone is not sufficient; consider how the source is used in the post.

**Choose personal_opinion** when the post primarily communicates personal experience, preference, reaction, judgment, or prediction. Predictions and opinions remain personal opinions even when stated confidently.

**Choose unsupported_claim** when the post primarily asserts a factual claim without an identifiable source or specific supporting evidence, and neither of the first two labels better describes its main purpose.

**Do not infer evidence** that is not present. Judge the text and its visible source attribution, not whether you personally believe the claim is true.

**Resolve overlap by primary purpose.** A post may contain both facts and opinions. Choose the label that best describes its main communicative purpose. Use the source-attribution rule when reporting sourced information is the main purpose; use the opinion rule when the author's perspective is the main purpose.

**Do not equate detail with evidence.** A long explanation, several examples, or confident wording does not automatically support a factual claim.

**Handle unclear or low-information posts consistently.** If a post contains too little information to classify confidently, flag it for review in the notes rather than inventing context or changing the definition to force a label.

## Scope

These labels describe the primary communicative purpose and support provided in a post. They do not independently determine whether a claim is true, whether a source is reliable, or whether an opinion is reasonable.