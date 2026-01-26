# GUT-Check Progressive Question Trigger Map

Version 0.3 — Aligned with Product Specification V0.3

## Purpose

This document defines when and why GUT-Check asks for progressive context during claim evaluation. It enforces the principle that **no question is asked unless it materially improves the analysis**.

## Core Rules (Non-Negotiable)

1. **Maximum 2 questions per response** (hard limit in JSON schema)
2. **All questions are optional** (enforced in schema with `optional: true`)
3. **Plain-language justification required** for every question
4. **Anonymous by default** - never require identification
5. **Progressive only** - no upfront forms

## Question Types

Based on Product Specification Section 4, the following question types are permitted:

- `age_range` - When evidence varies significantly by age
- `sex` - When biologically relevant to claim
- `location` - When regulatory/environmental factors matter
- `source` - Where user heard the claim (influence tracking)
- `motivation` - User's reason for asking (performance, health condition, etc.)
- `use_status` - Currently using vs considering
- `other` - Edge cases not covered above

## Trigger Map

### 1. Age Range Questions

**When to Ask:**
- Claim involves supplements/nutrients with age-dependent effects (e.g., calcium, vitamin D, creatine)
- Evidence shows different outcomes in different age groups
- Dosing or safety varies by life stage
- Regulatory guidance differs by age

**When NOT to Ask:**
- Claim is about general nutrition (e.g., "vegetables are healthy")
- Evidence is consistent across age groups
- Age already mentioned in user's query

**Example Justification:**
```json
{
  "question": "What is your age range?",
  "justification": "Creatine supplementation shows different safety profiles and effectiveness in adults over 65 versus younger adults. Your age range would help me identify the most relevant evidence.",
  "optional": true,
  "question_type": "age_range",
  "response_options": ["Under 18", "18-30", "31-50", "51-65", "Over 65", "Prefer not to say"]
}
```

**Claim Examples:**
- "Is creatine safe for older adults?"
- "Should I take vitamin D supplements?"
- "Are probiotics effective for children?"

---

### 2. Sex/Biological Sex Questions

**When to Ask:**
- Claim involves sex-specific biology (hormones, reproductive health, bone density)
- Evidence shows sex-differentiated outcomes
- Supplement affects sex hormones
- Safety profiles differ by sex

**When NOT to Ask:**
- Claim has no biological sex basis
- Evidence is sex-neutral
- Sex already mentioned in query

**Example Justification:**
```json
{
  "question": "What is your biological sex?",
  "justification": "Iron supplementation recommendations differ significantly between menstruating and non-menstruating individuals due to different baseline needs and deficiency risks.",
  "optional": true,
  "question_type": "sex",
  "response_options": ["Male", "Female", "Prefer not to say"]
}
```

**Claim Examples:**
- "Do I need iron supplements?"
- "Is soy protein safe?"
- "Should I take calcium for bone health?"

---

### 3. Location Questions

**When to Ask:**
- Claim involves regulatory differences (FDA vs EU regulations)
- Environmental factors matter (sunlight for vitamin D, altitude)
- Regional diet patterns affect baseline nutrition
- Product availability/legality varies by location

**When NOT to Ask:**
- Claim is about universal biological mechanisms
- Evidence doesn't vary geographically
- Regulatory status isn't relevant to the question

**Example Justification:**
```json
{
  "question": "What country or state are you in?",
  "justification": "CBD supplement regulations vary dramatically by location - some states classify it as legal, others restrict it, and the FDA has not approved it for most uses. Your location determines which products are legally available and what quality standards apply.",
  "optional": true,
  "question_type": "location",
  "response_options": ["United States", "Canada", "EU", "UK", "Australia", "Other", "Prefer not to say"]
}
```

**Claim Examples:**
- "Is CBD oil legal and safe?"
- "Can I get ivermectin?"
- "Do I need vitamin D supplements?" (latitude-dependent)

---

### 4. Source of Influence Questions

**When to Ask:**
- Claim appears to be marketing-driven or influencer-promoted
- Useful for tracking misinformation patterns (monetization via influence mapping)
- Pattern suggests commercial bias
- Source context helps assess claim framing

**When NOT to Ask:**
- User asks general research question
- Source is already stated in query
- Not relevant to evidence quality assessment

**Example Justification:**
```json
{
  "question": "Where did you hear about this claim?",
  "justification": "Understanding whether this claim comes from marketing, social media, medical advice, or research helps me assess whether the framing might be distorted by commercial incentives.",
  "optional": true,
  "question_type": "source",
  "response_options": ["Social media/influencer", "Advertisement", "Healthcare provider", "Friend/family", "News article", "Research paper", "Other", "Prefer not to say"]
}
```

**Claim Examples:**
- "I heard [product X] cures gut problems"
- "Should I try the [brand name] cleanse?"
- "Is [celebrity]'s supplement legit?"

---

### 5. Motivation Questions

**When to Ask:**
- Claim is broad and motivation helps narrow relevant evidence
- Different motivations have different evidence bases
- Risk assessment varies by use case (performance vs medical)
- User hasn't specified their goal

**When NOT to Ask:**
- Motivation is already clear from query
- Claim is narrow/specific
- All evidence applies regardless of motivation

**Example Justification:**
```json
{
  "question": "What's your primary reason for considering this?",
  "justification": "Probiotic evidence varies significantly by goal - gut health, immune function, mental health, and athletic performance all have different research bases and recommended strains.",
  "optional": true,
  "question_type": "motivation",
  "response_options": ["Digestive health", "Immune support", "Mental health", "Athletic performance", "General wellness", "Medical condition", "Other", "Prefer not to say"]
}
```

**Claim Examples:**
- "Should I take probiotics?"
- "Is beetroot juice worth it?"
- "Do I need magnesium supplements?"

---

### 6. Use Status Questions

**When to Ask:**
- Risk assessment differs for current users vs considering
- Safety monitoring is relevant for active users
- Stopping/continuing decision needs different evidence than starting decision
- Adverse effects or interactions are a concern

**When NOT to Ask:**
- Question is purely about efficacy, not safety
- Use status doesn't change the evidence assessment
- Already clear from query

**Example Justification:**
```json
{
  "question": "Are you currently using this, or considering starting?",
  "justification": "If you're already taking high-dose vitamin D, the relevant evidence shifts to monitoring for toxicity and adjusting dosage, versus if you're deciding whether to start, where we'd focus on deficiency risk and supplementation benefits.",
  "optional": true,
  "question_type": "use_status",
  "response_options": ["Currently using", "Considering starting", "Used in the past", "Just researching", "Prefer not to say"]
}
```

**Claim Examples:**
- "Is my supplement safe?"
- "Should I stop taking [X]?"
- "How much [supplement] should I take?"

---

## Question Prioritization Logic

When multiple questions could be asked, use this priority order:

### Priority 1: Questions that affect safety assessment
- Age (if age-dependent risks exist)
- Sex (if sex-specific risks exist)
- Use status (if currently taking something with risk)

### Priority 2: Questions that significantly narrow evidence scope
- Motivation (when evidence varies dramatically by goal)
- Location (when regulatory/legal status matters)

### Priority 3: Questions for tracking/monetization
- Source of influence (misinformation mapping)

**Never ask Priority 3 questions in the first response** unless no Priority 1 or 2 questions apply.

---

## Anti-Patterns (What NOT to Do)

### ❌ Don't ask fishing questions
**Bad:** "Tell me about yourself so I can give better advice"
**Why:** Violates progressive collection - not tied to specific analytical need

### ❌ Don't ask demographic questions for general claims
**Bad:** Asking age for "Are vegetables healthy?"
**Why:** Evidence doesn't vary enough to justify the question

### ❌ Don't ask multiple questions when one will do
**Bad:** Asking both age AND sex when only one affects the evidence
**Why:** Violates the 2-question maximum and progressive principle

### ❌ Don't ask questions when user already provided context
**Bad:** User says "I'm a 45-year-old woman" → asking age and sex
**Why:** Parse user input first; don't ask for information already given

### ❌ Don't frame questions as required
**Bad:** "I need to know your age to continue"
**Why:** All questions must be optional (enforced in schema)

### ❌ Don't ask without justification
**Bad:** Including question without explaining why it helps
**Why:** Violates transparency principle; required by schema

---

## Implementation Notes

### For AI/LLM Implementation:
1. Parse user query for context already provided
2. Evaluate claim type against trigger conditions
3. Identify which questions (if any) would materially improve analysis
4. Rank by priority order above
5. Select max 2 questions
6. Generate plain-language justification for each
7. Include in `next_questions` array in response JSON

### For Human Review:
- Each question should pass the "does this actually change my answer?" test
- If you can give the same quality analysis without the question, don't ask it
- Justification should convince a skeptical user that the question isn't just data collection

### For Testing:
Test cases should verify:
- No more than 2 questions per response
- All questions have `optional: true`
- All questions have non-empty `justification`
- Questions aren't asked for irrelevant claims
- Questions aren't asked when context already provided
- Same claim + same context = same questions (deterministic)

---

## Revision History

- **V0.3** - Aligned with Product Specification V0.3
- Added research_awareness context (doesn't trigger questions, but may affect confidence statements)
- Clarified that questions are for analysis improvement, not data collection

---

## Compliance Note

This trigger map enforces:
- Product Specification Section 4 (Progressive Context Collection Model)
- JSON Schema constraint: `maxItems: 2` on `next_questions`
- JSON Schema constraint: `optional: true` (constant) on all questions
- Privacy principles: anonymous-first, no required identification

Any question type or trigger condition not documented here is **out of scope** and should not be implemented.