# Biography Production System Architecture

## Executive Summary

This document defines an end-to-end system for producing biographies that satisfy two demanding standards simultaneously: academic rigor that withstands historian scrutiny, and narrative craft that engages general readers. The system treats biography as an evidence-based discipline with explicit rules for claims, verification, uncertainty, and ethical guardrails.

---

## System Overview: Information Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                           BIOGRAPHY PRODUCTION SYSTEM                                │
└─────────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 1: RESEARCH PIPELINE                                                          │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐                   │
│  │  QUESTION       │───▶│  SOURCE         │───▶│  SOURCE         │                   │
│  │  FRAMING        │    │  DISCOVERY      │    │  INTAKE         │                   │
│  │  ┌───────────┐  │    │  ┌───────────┐  │    │  ┌───────────┐  │                   │
│  │  │Thesis     │  │    │  │Primary    │  │    │  │Capture    │  │                   │
│  │  │Scope      │  │    │  │Secondary  │  │    │  │Metadata   │  │                   │
│  │  │Time bounds│  │    │  │Archives   │  │    │  │Tagging    │  │                   │
│  │  │Controversi│  │    │  │Interviews │  │    │  │Excerpts   │  │                   │
│  │  └───────────┘  │    │  └───────────┘  │    │  │CoC notes  │  │                   │
│  └─────────────────┘    └─────────────────┘    │  └───────────┘  │                   │
│                                                └────────┬────────┘                   │
│                                                         │                            │
│                                                         ▼                            │
│                                          ┌─────────────────────────┐                 │
│                                          │      SOURCE MAP         │                 │
│                                          │  (What supports what)   │                 │
│                                          └────────────┬────────────┘                 │
└───────────────────────────────────────────────────────┼─────────────────────────────┘
                                                        │
                                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 2: CLAIMS & EVIDENCE                                                          │
│  ┌─────────────────────────────────────────────────────────────────────────────┐    │
│  │                           CLAIM LEDGER                                       │    │
│  │  ┌─────────┬─────────┬────────────┬────────────┬─────────────┬───────────┐  │    │
│  │  │Claim ID │Type     │Confidence  │Supporting  │Counter-     │Citation   │  │    │
│  │  │         │FACT/INT/│VERIFIED/   │Sources     │Sources      │Format     │  │    │
│  │  │         │CONTEXT  │PROBABLE/..│[S001,S002] │[S003]       │Rules      │  │    │
│  │  └─────────┴─────────┴────────────┴────────────┴─────────────┴───────────┘  │    │
│  └─────────────────────────────────────────────────────────────────────────────┘    │
│                              │                                                       │
│         ┌────────────────────┼────────────────────┐                                 │
│         ▼                    ▼                    ▼                                 │
│  ┌─────────────┐      ┌─────────────┐      ┌─────────────┐                          │
│  │Citation     │      │Quotation    │      │Common       │                          │
│  │Standards    │      │Handling     │      │Knowledge    │                          │
│  │(FN/EN)      │      │Rules        │      │Filter       │                          │
│  └─────────────┘      └─────────────┘      └─────────────┘                          │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                                        │
                                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 3: VERIFICATION                                                               │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐                   │
│  │  TRIANGULATION  │───▶│  CONTRADICTION  │───▶│  RED TEAM       │                   │
│  │  ENGINE         │    │  RESOLUTION     │    │  PASS           │                   │
│  │  ┌───────────┐  │    │  ┌───────────┐  │    │  ┌───────────┐  │                   │
│  │  │Min sources│  │    │  │Playbook   │  │    │  │Disprove   │  │                   │
│  │  │by severity│  │    │  │execution  │  │    │  │key claims │  │                   │
│  │  │Date verify│  │    │  │Hierarchy  │  │    │  │Document   │  │                   │
│  │  │Name verify│  │    │  │rules      │  │    │  │attempts   │  │                   │
│  │  └───────────┘  │    │  └───────────┘  │    │  └───────────┘  │                   │
│  └─────────────────┘    └─────────────────┘    └─────────────────┘                   │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                                        │
                                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 4: UNCERTAINTY & ETHICS                                                       │
│  ┌───────────────────────────────────┐    ┌───────────────────────────────────┐     │
│  │  UNCERTAINTY TAXONOMY             │    │  ETHICS & BIAS CONTROLS           │     │
│  │  ┌─────────────────────────────┐  │    │  ┌─────────────────────────────┐  │     │
│  │  │UNKNOWN: No evidence exists  │  │    │  │Subject proximity audit      │  │     │
│  │  │AMBIGUOUS: Evidence unclear  │  │    │  │Presentism check             │  │     │
│  │  │CONTESTED: Sources disagree  │  │    │  │Hero/villain balance         │  │     │
│  │  │PROBABLE: Strong inference   │  │    │  │Missing voices review        │  │     │
│  │  │SPECULATIVE: Reasonable guess│  │    │  │Defamation risk check        │  │     │
│  │  └─────────────────────────────┘  │    │  │Interview ethics             │  │     │
│  │  Language: "likely" "appears"     │    │  └─────────────────────────────┘  │     │
│  │  "according to" "evidence suggests│    │                                    │     │
│  └───────────────────────────────────┘    └───────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                                        │
                                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 5: NARRATIVE DESIGN                                                           │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐                   │
│  │  SCENE          │    │  STRUCTURE      │    │  SCHOLARSHIP/   │                   │
│  │  CONSTRUCTION   │    │  PLAYBOOK       │    │  STORY BALANCE  │                   │
│  │  ┌───────────┐  │    │  ┌───────────┐  │    │  ┌───────────┐  │                   │
│  │  │Interiority│  │    │  │Acts       │  │    │  │Vivid but  │  │                   │
│  │  │limits     │  │    │  │Chapters   │  │    │  │accurate   │  │                   │
│  │  │Sensory    │  │    │  │Throughline│  │    │  │Engaging   │  │                   │
│  │  │constraints│  │    │  │Motifs     │  │    │  │but honest │  │                   │
│  │  │Evidence   │  │    │  │Character  │  │    │  │           │  │                   │
│  │  │basis      │  │    │  │network    │  │    │  │           │  │                   │
│  │  └───────────┘  │    │  └───────────┘  │    │  └───────────┘  │                   │
│  └─────────────────┘    └─────────────────┘    └─────────────────┘                   │
└─────────────────────────────────────────────────────────────────────────────────────┘
                                                        │
                                                        ▼
┌─────────────────────────────────────────────────────────────────────────────────────┐
│  PHASE 6: PRODUCTION STAGES WITH QUALITY GATES                                       │
│                                                                                      │
│  RESEARCH ──▶ GATE 1 ──▶ DRAFT ──▶ GATE 2 ──▶ VERIFY ──▶ GATE 3 ──▶ REVISE ──▶     │
│                                                                                      │
│  ──▶ GATE 4 ──▶ COPYEDIT ──▶ GATE 5 ──▶ FINAL MANUSCRIPT                            │
│                                                                                      │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Module 1: Research Pipeline

### 1.1 Question Framing

Before any source gathering, define the biography's intellectual foundation.

#### Question Framing Worksheet

```
PROJECT: _______________________________________________
SUBJECT: _______________________________________________
DATE INITIATED: ________________________________________

1. THESIS STATEMENT
   What argument does this biography make about its subject?
   (Not just "the life of X" but "X's life demonstrates/reveals/challenges...")

   Draft thesis: ________________________________________
   _____________________________________________________
   _____________________________________________________

   Thesis type:
   [ ] Corrective (revises prevailing view)
   [ ] Revelatory (surfaces unknown material)
   [ ] Synthetic (combines known material in new frame)
   [ ] Contextual (places subject in broader currents)

2. SCOPE DEFINITION

   Temporal bounds:
   - Start date/event: __________________________________
   - End date/event: ____________________________________
   - Justification for bounds: __________________________

   Thematic scope (check all that apply):
   [ ] Personal/psychological development
   [ ] Professional/career arc
   [ ] Public/political role
   [ ] Creative/intellectual output
   [ ] Relationships/networks
   [ ] Historical context/moment
   [ ] Other: __________________________________________

   Geographic scope: ____________________________________

   What is EXPLICITLY EXCLUDED and why:
   _____________________________________________________
   _____________________________________________________

3. TIME BOUNDS & PERIODIZATION

   Proposed life periods:
   Period 1: _____________ (years: _____ to _____)
   Period 2: _____________ (years: _____ to _____)
   Period 3: _____________ (years: _____ to _____)
   Period 4: _____________ (years: _____ to _____)
   Period 5: _____________ (years: _____ to _____)

   Key turning points to investigate:
   1. _________________________________________________
   2. _________________________________________________
   3. _________________________________________________
   4. _________________________________________________
   5. _________________________________________________

4. KEY CONTROVERSIES & CONTESTED TERRAIN

   List known debates about this subject:

   Controversy 1: _______________________________________
   - Position A: ________________________________________
   - Position B: ________________________________________
   - Your preliminary stance: ___________________________
   - Evidence needed to resolve: ________________________

   Controversy 2: _______________________________________
   - Position A: ________________________________________
   - Position B: ________________________________________
   - Your preliminary stance: ___________________________
   - Evidence needed to resolve: ________________________

   (Continue as needed)

5. EXISTING LITERATURE ASSESSMENT

   Previous biographies (list with assessment):
   - Title: _____________ Author: ________ Year: ________
     Strengths: _________________________________________
     Gaps: ______________________________________________

   (Continue for all major works)

   What does your biography add that doesn't exist?
   _____________________________________________________
   _____________________________________________________

6. RESEARCH QUESTIONS

   Primary question (what must be answered):
   _____________________________________________________

   Secondary questions:
   1. _________________________________________________
   2. _________________________________________________
   3. _________________________________________________
   4. _________________________________________________
   5. _________________________________________________

   Questions you suspect cannot be answered (and why):
   1. _________________________________________________
   2. _________________________________________________
```

### 1.2 Source Discovery

#### Source Categories and Search Protocol

| Category | Definition | Search Methods | Reliability Notes |
|----------|------------|----------------|-------------------|
| **PRIMARY - Level 1** | Created by subject | Archive catalogs, estate papers, institutional collections | Highest authority for subject's views; beware self-fashioning |
| **PRIMARY - Level 2** | Created during subject's lifetime by contemporaries | Newspaper archives, court records, correspondence collections | Authority varies by creator's access; cross-check dates |
| **SECONDARY - Level 1** | Scholarly works with primary research | Academic databases, bibliographies | Verify claims against cited sources |
| **SECONDARY - Level 2** | Derivative works, journalism | Library catalogs, news archives | Use for leads, not as authority |
| **ORAL - Level 1** | First-person accounts from subject or direct witnesses | Interviews, oral history archives | Time decay; memory construction; verify against documents |
| **ORAL - Level 2** | Secondhand accounts | Interviews with those who knew witnesses | Use cautiously; verify any factual claims |

#### Source Discovery Checklist

```
SUBJECT: _____________________________________________
RESEARCH PHASE: [ ] Initial [ ] Deep [ ] Gap-filling

ARCHIVES & REPOSITORIES

Personal Papers:
[ ] Subject's personal archive (location: _______________)
    Status: [ ] Identified [ ] Access requested [ ] Visited [ ] Exhausted
    Finding aid reviewed: [ ] Yes [ ] No [ ] N/A

[ ] Family collections (contact: _______________________)
    Status: [ ] Identified [ ] Access requested [ ] Visited [ ] Exhausted

[ ] Estate/literary executor (contact: __________________)
    Status: [ ] Identified [ ] Access requested [ ] Visited [ ] Exhausted

Institutional Archives:
[ ] Employer/workplace records (institution: ___________)
    Status: [ ] Identified [ ] Access requested [ ] Visited [ ] Exhausted

[ ] Educational institutions attended:
    - Institution: _____________ Status: ________________
    - Institution: _____________ Status: ________________

[ ] Professional organizations (list: __________________)
    Status: [ ] Identified [ ] Access requested [ ] Visited [ ] Exhausted

Government Records:
[ ] Birth/death certificates      Source: ______________
[ ] Marriage/divorce records      Source: ______________
[ ] Immigration/naturalization    Source: ______________
[ ] Military service records      Source: ______________
[ ] Tax records (if available)    Source: ______________
[ ] Property records              Source: ______________
[ ] Court records (civil)         Source: ______________
[ ] Court records (criminal)      Source: ______________
[ ] FBI/intelligence files (FOIA) Status: ______________

PUBLISHED SOURCES

Newspapers:
[ ] Major newspapers of subject's location(s)
    Papers searched: ___________________________________
    Date ranges: _______________________________________
    Search terms used: _________________________________

[ ] Trade/specialty publications relevant to subject's field
    Publications: ______________________________________

Periodicals:
[ ] Contemporary magazines
    Titles searched: ___________________________________

[ ] Academic journals
    Databases searched: ________________________________

Books:
[ ] Previous biographies (list in Question Framing)
[ ] Memoirs mentioning subject
    Titles: ___________________________________________
[ ] Historical works covering subject's era/field
    Titles: ___________________________________________

INTERVIEWS

Living Sources:
[ ] Family members
    - Name: _____________ Relation: ______ Status: ______
    - Name: _____________ Relation: ______ Status: ______

[ ] Friends/intimates
    - Name: _____________ Period known: ___ Status: _____

[ ] Professional colleagues
    - Name: _____________ Context: ______ Status: ______

[ ] Other witnesses
    - Name: _____________ Relevance: ____ Status: ______

Existing Oral Histories:
[ ] Oral history archives checked:
    - Archive: _____________ Result: ___________________
    - Archive: _____________ Result: ___________________

VISUAL/MATERIAL SOURCES

[ ] Photographs (location: ____________________________)
[ ] Film/video footage (location: _____________________)
[ ] Audio recordings (location: _______________________)
[ ] Artwork by/depicting subject (location: ___________)
[ ] Physical objects/artifacts (location: ______________)

DIGITAL SOURCES

[ ] Email archives (access status: ____________________)
[ ] Social media archives (platforms: __________________)
[ ] Digital correspondence (status: ____________________)
[ ] Website archives (Wayback Machine, etc.): __________

GAP ANALYSIS

Sources sought but not found:
1. _________________________________________________
2. _________________________________________________
3. _________________________________________________

Sources known to exist but inaccessible:
1. _________________ Reason: _________________________
2. _________________ Reason: _________________________

Sources destroyed/lost:
1. _________________ Evidence: _______________________
2. _________________ Evidence: _______________________
```

### 1.3 Source Intake Workflow

Every source that enters the research database must pass through standardized intake.

#### Source Intake Form (Template in separate file: `templates/source_intake_form.md`)

**Process Steps:**

1. **Capture**: Obtain physical or digital copy
   - Photograph/scan documents
   - Record audio/video of interviews
   - Download digital materials
   - Create archival-quality copies

2. **Assign Source ID**: Format `S-[TYPE]-[YEAR]-[SEQUENCE]`
   - Types: DOC (document), INT (interview), PUB (publication), GOV (government), IMG (image), AUD (audio), VID (video)
   - Example: `S-DOC-1952-001`

3. **Complete Metadata Fields**: (See template)

4. **Tag for Themes/Topics**: Use controlled vocabulary
   - Create project-specific tag taxonomy before research begins
   - Minimum tags: time period, location, people mentioned, topics

5. **Extract Quotes/Excerpts**:
   - Transcribe relevant passages verbatim
   - Include page/paragraph/timestamp locators
   - Note context surrounding excerpt

6. **Chain-of-Custody Notes**:
   - Where did you find this?
   - Who gave you access?
   - What restrictions apply?
   - What is the provenance?

7. **Initial Reliability Assessment**:
   - Primary or secondary?
   - Creator's relationship to events?
   - Time gap between event and creation?
   - Known biases or agendas?
   - Corroborating sources exist?

### 1.4 Source Map Construction

A source map shows what evidence supports what claims, enabling you to see the evidentiary foundation of your entire argument.

#### Source Map Structure

```
SOURCE MAP: [Project Name]
Generated: [Date]
Version: [X.X]

═══════════════════════════════════════════════════════════════
THESIS-LEVEL SUPPORT
═══════════════════════════════════════════════════════════════

Thesis: [Your thesis statement]

Supporting source clusters:
┌─────────────────────────────────────────────────────────────┐
│ Cluster A: [Theme]                                          │
│   └── S-DOC-1952-001: [Brief description]                  │
│   └── S-INT-2023-005: [Brief description]                  │
│   └── S-PUB-1965-002: [Brief description]                  │
│   Cluster strength: [STRONG/MODERATE/WEAK]                  │
│   Notes: _________________________________________________ │
├─────────────────────────────────────────────────────────────┤
│ Cluster B: [Theme]                                          │
│   └── [Sources]                                             │
│   Cluster strength: [STRONG/MODERATE/WEAK]                  │
└─────────────────────────────────────────────────────────────┘

Counter-evidence to thesis:
┌─────────────────────────────────────────────────────────────┐
│ Counter-cluster: [Description]                              │
│   └── S-XXX-XXXX-XXX: [Brief description]                  │
│   How addressed: _________________________________________ │
└─────────────────────────────────────────────────────────────┘

═══════════════════════════════════════════════════════════════
CHAPTER-LEVEL SOURCE MAPS
═══════════════════════════════════════════════════════════════

CHAPTER 1: [Title]
Central claim: _____________________________________________

  Claim 1.1: [Claim text]
  ├── Type: [FACT/INTERPRETATION/CONTEXT]
  ├── Supporting: S-XXX-XXXX-XXX (p. XX), S-XXX-XXXX-XXX (p. XX)
  ├── Counter: [None / Source IDs]
  └── Confidence: [VERIFIED/PROBABLE/CONTESTED/SPECULATIVE]

  Claim 1.2: [Claim text]
  ├── Type: [FACT/INTERPRETATION/CONTEXT]
  ├── Supporting: [Source IDs with locations]
  ├── Counter: [None / Source IDs]
  └── Confidence: [Level]

(Continue for each claim in chapter)

═══════════════════════════════════════════════════════════════
EVIDENCE GAPS
═══════════════════════════════════════════════════════════════

Claims with single-source support (vulnerability list):
1. Claim X.X: [Claim text] - Only source: S-XXX-XXXX-XXX
   Action needed: _________________________________________

Claims with no direct evidence (inference-based):
1. Claim X.X: [Claim text] - Basis for inference: ________
   Acknowledged in text: [ ] Yes [ ] No

═══════════════════════════════════════════════════════════════
SOURCE RELIABILITY TIERS
═══════════════════════════════════════════════════════════════

Tier 1 (Highest reliability):
- S-XXX-XXXX-XXX: [Brief description]
- S-XXX-XXXX-XXX: [Brief description]

Tier 2 (Reliable with caveats):
- S-XXX-XXXX-XXX: [Brief description] - Caveat: ___________

Tier 3 (Use cautiously):
- S-XXX-XXXX-XXX: [Brief description] - Limitation: _______

Tier 4 (Background only):
- S-XXX-XXXX-XXX: [Brief description] - Why limited: ______
```

---

## Module 2: Claims, Evidence, and Citations

### 2.1 Claim Ledger Model

Every factual or interpretive statement in the biography should have a corresponding entry in the Claim Ledger (or fall under "common knowledge" exemption).

#### Claim Ledger Entry Structure

**See template file: `templates/claim_ledger_entry.md`**

#### Claim Types

| Type | Code | Definition | Citation Requirement | Confidence Threshold |
|------|------|------------|---------------------|---------------------|
| **FACT** | F | Verifiable event, date, name, location, action | Required | Must be VERIFIED or PROBABLE |
| **INTERPRETATION** | I | Analysis, meaning, causation, motivation | Required + attribution | Can be CONTESTED if acknowledged |
| **CONTEXT** | C | Historical background, setting, conditions | Required for specific claims | VERIFIED or PROBABLE |
| **QUOTATION** | Q | Direct words of subject or others | Required with exact source | Must be VERIFIED |
| **SCENE** | S | Reconstructed narrative moment | Required + constraints noted | See Scene Construction Rules |

#### Confidence Levels

| Level | Code | Definition | Source Requirements | Narrative Handling |
|-------|------|------------|---------------------|-------------------|
| **VERIFIED** | V | Multiple independent sources confirm; no contradicting evidence | 2+ independent primary sources | State as fact |
| **PROBABLE** | P | Strong evidence from reliable source(s); no significant contradicting evidence | 1 high-reliability primary or 2+ secondary | State as fact or with minimal hedging |
| **CONTESTED** | CT | Sources disagree; scholarly debate exists | Present all significant positions | "According to X... however, Y argues..." |
| **SPECULATIVE** | SP | Reasonable inference from available evidence, but not directly supported | Inference chain documented | "It seems likely that..." "Evidence suggests..." |
| **UNKNOWN** | U | No evidence exists | N/A | Acknowledge gap or omit |

### 2.2 Citation Standards

#### Citation Format Rules

**Footnotes vs. Endnotes Decision Matrix:**

| Factor | Choose Footnotes | Choose Endnotes |
|--------|-----------------|-----------------|
| Academic audience primary | ✓ | |
| General audience primary | | ✓ |
| Notes contain substantive discussion | ✓ | |
| Notes are purely citations | | ✓ |
| Publisher preference | Follow | Follow |
| High controversy content | ✓ (visibility) | |

**Citation Completeness Requirements:**

For ARCHIVAL sources:
```
[Collection Name], [Box/Folder], [Document Title if any], [Date],
[Repository Name], [City].
```

For PUBLISHED sources (follow Chicago 17th):
```
Author Last, First. Title. Place: Publisher, Year. Page(s).
```

For INTERVIEWS:
```
[Interviewee Name], interview by [Interviewer], [Date], [Location/medium],
[Recording/transcript location if archived].
```

For NEWSPAPERS:
```
[Author if known], "[Article Title]," [Newspaper Name], [Date], [Page/Section].
```

**Page/Location Precision Rules:**

| Source Type | Minimum Precision | Example |
|-------------|-------------------|---------|
| Books | Page number | p. 47 |
| Long documents | Page + paragraph if needed | p. 12, para. 3 |
| Manuscripts | Folio/page + recto/verso | fol. 23r |
| Newspapers | Page, column if possible | p. A3, col. 2 |
| Audio/video | Timestamp | 23:45-24:12 |
| Interviews | Timestamp or transcript page | transcript p. 15 |
| Websites | Full URL + access date | [URL], accessed Jan 8, 2026 |

### 2.3 Quotation Handling Rules

**Direct Quotation Rules:**

1. **Verbatim accuracy**: Reproduce exactly as in source, including errors
   - Use [sic] for errors in original
   - Use [...] for omissions within quote
   - Use [word] for clarifying insertions

2. **Context preservation**: Quote must not misrepresent meaning
   - Check surrounding text
   - Note if ironic, sarcastic, or qualified in original

3. **Source verification**: For secondhand quotes (quoted in another source)
   - Always attempt to find original source
   - If using secondhand: "quoted in [Source]"
   - Note if original unavailable

4. **Length thresholds**:
   - Under 40 words: Inline with quotation marks
   - 40+ words: Block quote format
   - Consider paraphrase for very long passages

**Paraphrase Rules:**

1. **Genuine transformation**: Must be your words, not minor substitutions
2. **Meaning fidelity**: Must accurately represent original meaning
3. **Citation required**: Always cite paraphrased material
4. **Distinguish from summary**: Paraphrase = specific passage; Summary = overall argument

### 2.4 Common Knowledge Filter

**Does NOT require citation:**

- Birth/death dates findable in standard references
- Major historical events (wars, elections) with well-known dates
- Geographic facts (city locations, etc.)
- Definitions of common terms
- Subject's publicly known basic biography (positions held, major published works)

**REQUIRES citation even if "well known":**

- Any disputed fact, even if one version is widely repeated
- Any number (statistics, amounts, measurements)
- Any quotation
- Any interpretation or characterization
- Any detail that enhances or undermines subject's reputation
- Anything you learned from research (if you had to look it up, cite it)

**When in doubt: CITE.**

---

## Module 3: Verification and Fact-Checking

### 3.1 Triangulation Rules

**Minimum Corroboration Thresholds by Claim Severity:**

| Claim Category | Minimum Sources | Source Requirements |
|----------------|-----------------|---------------------|
| **Neutral fact** (date, location, name) | 1 reliable primary OR 2 secondary | Independence not required |
| **Positive characterization** (praise, achievement) | 1 reliable | Note if self-reported |
| **Negative characterization** (criticism, failure) | 2 independent | Not both from hostile sources |
| **Controversial claim** | 3 independent | At least 1 primary |
| **Potentially defamatory** | 3+ independent | Multiple primaries preferred |
| **Criminal/illegal behavior** | 3+ independent | Strong preference for documents over recollection |
| **Private/intimate life** | 2+ independent | At least 1 near-contemporaneous |
| **Internal state/motivation** | See Interiority Rules | Special handling required |

**Independence Definition:**
Sources are independent if:
- They did not derive information from each other
- They do not share a common biased source
- They had separate access to the information

### 3.2 Verification Workflow

#### Date Verification Protocol

```
CLAIM: [Event] occurred on [Date]

Step 1: Identify date source
- Source claiming date: ________________________________
- Source type: [ ] Primary [ ] Secondary
- Source's likely knowledge basis: _____________________

Step 2: Check for corroboration
- Second source: ______________________________________
- Date matches: [ ] Yes [ ] No [ ] Partial
- If partial, discrepancy: _____________________________

Step 3: Check for contradictions
- Contradicting sources: _______________________________
- Discrepancy: ________________________________________

Step 4: Resolve discrepancies (if any)
- Most reliable source: _______________________________
- Reasoning: __________________________________________

Step 5: Assign confidence
[ ] VERIFIED (multiple independent sources agree)
[ ] PROBABLE (reliable source, no contradiction)
[ ] CONTESTED (sources disagree)
[ ] APPROXIMATE (use "circa," "around," "by")

Final date to use: ____________________________________
Note for text: ________________________________________
```

#### Name Verification Protocol

```
CLAIM: Person's name is [Name]

Step 1: Identify naming source
- Source: _____________________________________________
- Full name given: ____________________________________
- Name variations encountered: _________________________

Step 2: Check official records
- Birth certificate: __________________________________
- Other government records: ____________________________
- Consistent: [ ] Yes [ ] No

Step 3: Subject's self-identification
- How did subject refer to themselves? _________________
- Did this change over time? __________________________

Step 4: Resolve variations
- Legal name: _________________________________________
- Preferred name: _____________________________________
- Name used in text: __________________________________
- First reference note: _______________________________
```

#### Location Verification Protocol

```
CLAIM: [Event] occurred at [Location]

Step 1: Identify location source
- Source: _____________________________________________
- Specificity: [ ] Address [ ] City [ ] Region [ ] Country

Step 2: Verify location existed
- Location exists/existed: [ ] Yes [ ] No [ ] Changed
- If changed, status at time of event: _________________

Step 3: Verify subject's presence
- Evidence of presence: _______________________________
- Dates of presence: __________________________________

Step 4: Check for contradicting locations
- Other claimed locations for same event: ______________
- Resolution: _________________________________________
```

#### Quote Verification Protocol

```
QUOTE: "[Quote text]"
ATTRIBUTED TO: ________________________________________
CONTEXT: _____________________________________________

Step 1: Trace to earliest source
- Source where you found quote: _______________________
- Earlier source cited: _______________________________
- Earliest source found: ______________________________
- Original source located: [ ] Yes [ ] No

Step 2: Verify exact wording
- Does earliest source match? [ ] Yes [ ] No
- Variations found: ___________________________________

Step 3: Verify attribution
- Did this person actually say/write this? _____________
- Evidence: __________________________________________
- Misattribution risk: [ ] Low [ ] Medium [ ] High

Step 4: Verify context
- Original context: ___________________________________
- Does use preserve meaning: [ ] Yes [ ] No [ ] Partial

Step 5: Decision
[ ] Use as direct quote with citation to original
[ ] Use as direct quote with "quoted in" citation
[ ] Paraphrase (original unavailable/uncertain)
[ ] Do not use (verification failed)

Note for text: ________________________________________
```

### 3.3 Contradiction Resolution Playbook

When sources disagree, follow this decision tree:

```
CONTRADICTION IDENTIFIED

Step 1: Classify the contradiction
[ ] FACTUAL: Sources give different facts (dates, names, events)
[ ] INTERPRETIVE: Sources agree on facts but differ on meaning
[ ] PARTIAL: Sources agree on some elements, differ on others

Step 2: Assess source reliability hierarchy
For factual contradictions, generally prefer:
1. Contemporary documents over later recollections
2. Multiple independent sources over single source
3. Official records over informal accounts
4. Disinterested parties over interested parties
5. Consistent accounts over accounts that changed
6. Specific details over vague claims

For the specific contradiction:
- Source A reliability factors: _________________________
- Source B reliability factors: _________________________
- Hierarchy suggests: __________________________________

Step 3: Look for resolution evidence
- Is there a third source? _____________________________
- Can discrepancy be explained? (Typo, different calendar,
  different event, etc.): _______________________________
- Did one source have better access? ___________________

Step 4: Make decision

[ ] RESOLUTION FOUND:
    Correct version: ___________________________________
    Evidence: __________________________________________
    How handled in text: _______________________________

[ ] RESOLUTION FAVORS ONE VERSION:
    Preferred version: _________________________________
    Reasoning: _________________________________________
    How handled in text: _______________________________
    Note other version: [ ] Yes (footnote) [ ] No (weak)

[ ] RESOLUTION NOT POSSIBLE:
    Present both versions in text: [ ] Yes [ ] No
    If yes, framing: __________________________________
    If no, reasoning: __________________________________

Step 5: Document for readers
- Is reader told of uncertainty? [ ] Yes [ ] No
- If no, justification: ________________________________
```

### 3.4 Red Team Pass

After completing verification, conduct adversarial review of key claims.

#### Red Team Protocol

```
RED TEAM REVIEW
Conducted by: ________________________________________
Date: ________________________________________________
Chapter/Section: _____________________________________

OBJECTIVE: Systematically attempt to disprove or undermine
key claims before hostile reviewers do.

═══════════════════════════════════════════════════════════
KEY CLAIM 1: [State claim]
═══════════════════════════════════════════════════════════

Current evidence base:
- Primary sources: ____________________________________
- Secondary sources: __________________________________
- Interview evidence: _________________________________

ATTACK VECTORS:

1. Source credibility attack:
   Q: What would undermine our sources' credibility?
   A: ______________________________________________
   Searched for evidence of this: [ ] Yes [ ] No
   Result: _________________________________________

2. Alternative explanation attack:
   Q: What else could explain this evidence?
   A: ______________________________________________
   Evidence for alternatives: _______________________
   Result: _________________________________________

3. Missing evidence attack:
   Q: What evidence should exist if claim is true?
   A: ______________________________________________
   Does it exist: [ ] Yes [ ] No [ ] Unknown
   If no, concerning: [ ] Yes [ ] No

4. Motivated reasoning check:
   Q: Do we want this to be true?
   A: [ ] Yes [ ] No [ ] Neutral
   If yes, extra scrutiny applied: [ ] Yes

5. Counter-source search:
   Q: Who would contradict this and have we looked?
   Searched: ________________________________________
   Found: __________________________________________

VERDICT FOR CLAIM 1:
[ ] SURVIVES RED TEAM (evidence withstands scrutiny)
[ ] NEEDS STRENGTHENING (action: ___________________)
[ ] NEEDS HEDGING (language change: ________________)
[ ] SHOULD BE CUT (reasoning: _____________________)

(Repeat for each key claim)

═══════════════════════════════════════════════════════════
OVERALL RED TEAM ASSESSMENT
═══════════════════════════════════════════════════════════

Total key claims reviewed: ________
Survived intact: ________
Needed strengthening: ________
Needed hedging: ________
Cut: ________

Most vulnerable argument in manuscript:
___________________________________________________
Action taken: ______________________________________

Strongest argument in manuscript:
___________________________________________________

Areas where hostile reviewer could attack:
1. ________________________________________________
   Preemptive action: _______________________________
2. ________________________________________________
   Preemptive action: _______________________________
```

---

## Module 4: Uncertainty Done Well

### 4.1 Uncertainty Taxonomy

| Category | Code | Definition | Source Situation | Reader Impact |
|----------|------|------------|------------------|---------------|
| **UNKNOWN** | UNK | No evidence exists; we cannot know | No sources found despite search | Gap acknowledged or omitted |
| **AMBIGUOUS** | AMB | Evidence exists but meaning unclear | Sources don't clearly indicate | Ambiguity presented honestly |
| **CONTESTED** | CON | Sources actively disagree | Multiple sources, different claims | Multiple views presented |
| **PROBABLE** | PRB | Strong inference, not direct evidence | Evidence supports but doesn't prove | Qualified statement |
| **SPECULATIVE** | SPC | Reasonable conjecture beyond evidence | Limited evidence extrapolated | Clear hedging language |

### 4.2 Uncertainty Language Guide

**PROHIBITED hedging (too vague, weakens without informing):**
- "Perhaps"
- "Maybe"
- "It is possible that"
- "One might think"
- "It could be argued"

**REQUIRED hedging formats (informative uncertainty):**

For PROBABLE claims:
- "Evidence strongly suggests that..."
- "By [X date], [subject] had likely..."
- "The available evidence points to..."
- "Though not documented, [X] almost certainly..."

For SPECULATIVE claims:
- "While no direct evidence survives, [reasoning] suggests..."
- "If [documented fact] is any indication, [subject] may have..."
- "Given [context], it seems reasonable that..."
- "One plausible explanation is..."

For CONTESTED claims:
- "According to [Source A], [claim]. However, [Source B] maintains that..."
- "Scholars disagree about [X]: [Position 1] vs. [Position 2]"
- "The traditional account holds that [X], though recent evidence suggests..."
- "[Subject] claimed [X], but contemporaries disputed this"

For AMBIGUOUS claims:
- "The meaning of [evidence] remains unclear"
- "Whether [X] indicates [Y] or [Z] cannot be determined"
- "This could indicate [A], though [B] is equally possible"

For UNKNOWN:
- "No record of [X] survives" (if relevant)
- Simply omit (if not essential)
- "What [subject] thought about [X] is lost to history"

### 4.3 Uncertainty Integration Guidelines

**When to be explicit about uncertainty:**
- The uncertain element is important to your argument
- Readers might assume certainty where none exists
- Other accounts present uncertain claims as facts
- The uncertainty itself is historically significant

**When uncertainty can be implicit:**
- Minor details where exactness isn't important
- Standard historical reconstruction readers expect
- The uncertain element isn't bearing argumentative weight

**Maintaining reader trust:**
- Be consistent: don't hedge minor claims then state major claims baldly
- Front-load acknowledgment of limitations in introduction
- Use notes for extended methodological discussion
- Distinguish your uncertainty from genuine historical mystery

---

## Module 5: Ethics and Bias Controls

### 5.1 Subject Proximity Assessment

```
SUBJECT PROXIMITY AUDIT

1. Personal connection inventory
   [ ] I knew/know the subject personally
   [ ] I knew/know the subject's family
   [ ] I share the subject's profession/field
   [ ] I share the subject's political/ideological views
   [ ] I share the subject's demographic characteristics
   [ ] I have published views on the subject before
   [ ] I have personal/professional stake in conclusions

   If any checked, complete mitigation plan:
   Connection: ________________________________________
   Potential bias: ____________________________________
   Mitigation: ________________________________________

2. Emotional relationship audit
   At project start, my feelings toward subject were:
   [ ] Admiring [ ] Neutral [ ] Critical [ ] Mixed

   At current stage, my feelings are:
   [ ] Admiring [ ] Neutral [ ] Critical [ ] Mixed

   If changed, reflect: ________________________________
   ____________________________________________________

3. Access considerations
   Did subject/estate grant access? [ ] Yes [ ] No [ ] N/A
   If yes, any conditions? _____________________________
   Could this bias presentation? _______________________
   Mitigation: ________________________________________
```

### 5.2 Presentism Check

```
PRESENTISM REVIEW

For each chapter, audit for anachronistic judgment:

Chapter: _____________________________________________

1. Moral standards applied:
   [ ] Judging past actions by present moral standards
   Examples found: ____________________________________
   Revision needed: ___________________________________

2. Knowledge assumptions:
   [ ] Assuming subject knew things only clear in hindsight
   Examples found: ____________________________________
   Revision needed: ___________________________________

3. Teleology:
   [ ] Presenting events as inevitably leading to known outcome
   Examples found: ____________________________________
   Revision needed: ___________________________________

4. Language:
   [ ] Using anachronistic terminology
   Examples found: ____________________________________
   Revision needed: ___________________________________

5. Context provided:
   [ ] Period norms adequately explained
   [ ] Reader can understand actions in period context
   [ ] Judgment clearly distinguished from description
```

### 5.3 Hero/Villain Framing Audit

```
FRAMING BALANCE CHECK

1. Positive moment inventory:
   List subject's achievements/virtues emphasized:
   1. ________________________________________________
   2. ________________________________________________
   3. ________________________________________________

2. Negative moment inventory:
   List subject's failures/flaws emphasized:
   1. ________________________________________________
   2. ________________________________________________
   3. ________________________________________________

3. Balance assessment:
   [ ] Skews hagiographic (too positive)
   [ ] Skews hostile (too negative)
   [ ] Appropriately balanced
   [ ] Intentionally positioned (justified: ___________)

4. Agency distribution:
   Subject's successes attributed to:
   [ ] Primarily their skill/effort
   [ ] Primarily external factors
   [ ] Balanced

   Subject's failures attributed to:
   [ ] Primarily their flaws/choices
   [ ] Primarily external factors
   [ ] Balanced

   Asymmetry detected: [ ] Yes [ ] No
   If yes, justified: [ ] Yes [ ] No

5. Comparative framing:
   Is subject compared to contemporaries: [ ] Yes [ ] No
   If yes, comparison fair: [ ] Yes [ ] No
   Revision needed: ___________________________________
```

### 5.4 Selective Evidence Audit

```
EVIDENCE SELECTION REVIEW

1. Source diversity check:
   Perspectives represented in source base:
   [ ] Subject's own voice
   [ ] Supporters/admirers
   [ ] Critics/opponents
   [ ] Neutral observers
   [ ] Affected parties
   [ ] Institutional voices
   [ ] Subordinates/less powerful figures

   Missing perspectives: ______________________________
   Attempted to find: [ ] Yes [ ] No
   If not found, explained: [ ] Yes [ ] No

2. Cherry-picking check:
   For each major claim, were contradicting sources:
   [ ] Sought
   [ ] Found but not used (justify: __________________)
   [ ] Found and addressed
   [ ] Not found

3. Negative space analysis:
   Important events/periods with thin sourcing:
   1. ________________________________________________
      Acknowledged to reader: [ ] Yes [ ] No
   2. ________________________________________________
      Acknowledged to reader: [ ] Yes [ ] No
```

### 5.5 Interview Ethics Protocol

```
INTERVIEW ETHICS CHECKLIST

PRE-INTERVIEW:
[ ] Purpose of interview explained to subject
[ ] How information may be used explained
[ ] Publication context explained
[ ] Recording permission obtained
[ ] Written consent obtained (required for: ___________)
[ ] Right to review quotes explained
[ ] Confidentiality terms agreed:
    [ ] On record
    [ ] On background
    [ ] Off record
    Terms documented: ________________________________

DURING INTERVIEW:
[ ] Stay within agreed scope
[ ] Note any off-record requests
[ ] Distinguish fact claims from opinions
[ ] Probe but don't manipulate
[ ] Note emotional state/duress concerns

POST-INTERVIEW:
[ ] Provide quote review if promised
[ ] Honor any retraction requests (within reason)
[ ] Secure recording/transcript
[ ] Document consent trail

SPECIAL CONSIDERATIONS:
Vulnerable subjects: _________________________________
Power dynamics: _____________________________________
Trauma-related content: ______________________________
```

### 5.6 Privacy and Defamation Risk Assessment

```
PRIVACY/DEFAMATION REVIEW

For each potentially sensitive claim:

Claim: _______________________________________________

1. Privacy assessment:
   Subject status: [ ] Public figure [ ] Private person
   Information type: [ ] Public record [ ] Private life
   Legitimate interest: [ ] High [ ] Medium [ ] Low
   Consent: [ ] Given [ ] Not sought [ ] Refused
   Deceased: [ ] Yes [ ] No (if yes, consider family)

   Privacy risk: [ ] Low [ ] Medium [ ] High
   Action: ___________________________________________

2. Defamation risk (for living subjects or recent dead):
   Statement of fact or opinion: [ ] Fact [ ] Opinion
   Defamatory meaning: [ ] Yes [ ] No [ ] Possibly
   Truth defense:
   - Can prove true: [ ] Yes [ ] No [ ] Probably
   - Evidence: ________________________________________

   Defamation risk: [ ] Low [ ] Medium [ ] High
   Legal review needed: [ ] Yes [ ] No
   Action: ___________________________________________

3. Third-party considerations:
   Others identifiable: [ ] Yes [ ] No
   Their consent: [ ] Given [ ] Not sought [ ] Refused
   Potential harm: ____________________________________
   Action: ___________________________________________
```

### 5.7 Missing Voices Review

```
MISSING VOICES AUDIT

1. Identity categories relevant to subject's life:
   (Check all that apply to people in subject's orbit)
   [ ] Women
   [ ] Racial/ethnic minorities
   [ ] Working class/poor
   [ ] LGBTQ+ individuals
   [ ] Non-Western perspectives
   [ ] Disabled individuals
   [ ] Children
   [ ] Religious minorities
   [ ] Other: ________________________________________

2. For each checked category:
   Category: _________________________________________
   Present in narrative: [ ] Yes [ ] No [ ] Minimal
   Source availability: [ ] Good [ ] Limited [ ] None
   If limited/none, why: ______________________________
   What was attempted: ________________________________
   Acknowledged in text: [ ] Yes [ ] No

3. Power dynamic assessment:
   Whose stories are told primarily through:
   [ ] Their own words
   [ ] Subject's words about them
   [ ] Other observers' words

   Who lacks their own voice: _________________________
   Mitigation: ________________________________________

4. Structural silences:
   What groups were systematically excluded from:
   - Archives: ________________________________________
   - Published record: ________________________________
   - Subject's known circle: ___________________________

   How handled: _______________________________________
```

### 5.8 Bias Audit Checklist

```
COMPREHENSIVE BIAS AUDIT

Auditor: _____________________________________________
Date: ________________________________________________
Manuscript version: ___________________________________

SECTION 1: AUTHOR POSITION
[ ] Subject proximity audit completed
[ ] Personal stakes disclosed in acknowledgments
[ ] Previous positions on subject disclosed

SECTION 2: FRAMING
[ ] Hero/villain audit completed
[ ] Presentism check completed
[ ] Agency distribution balanced
[ ] Opening/closing don't over-determine reading

SECTION 3: EVIDENCE
[ ] Selective evidence audit completed
[ ] Contradicting sources addressed
[ ] Source base diversity assessed
[ ] Gaps acknowledged

SECTION 4: VOICES
[ ] Missing voices review completed
[ ] Power dynamics considered
[ ] Structural silences acknowledged

SECTION 5: LANGUAGE
[ ] Loaded terms flagged and reviewed
[ ] Adjective audit (do modifiers smuggle judgment?)
[ ] Passive voice not hiding agency inappropriately

SECTION 6: STRUCTURE
[ ] Chapter order doesn't create false causation
[ ] Pacing doesn't minimize important events
[ ] Balance of coverage across life periods justified

OVERALL ASSESSMENT:
Significant bias concerns: ____________________________
Revisions made: ______________________________________
Residual issues acknowledged: _________________________

Sign-off: ____________________________________________
```

---

## Module 6: Narrative Design

### 6.1 Scene Construction Rules

Scenes bring biography to life but require evidential grounding.

#### Scene Construction Protocol

```
SCENE WORKSHEET

Scene location in manuscript: Chapter __ , Section __
Scene date/period: ___________________________________
Scene location: ______________________________________
Scene purpose (what it shows): _______________________

═══════════════════════════════════════════════════════════
EVIDENCE BASE FOR SCENE
═══════════════════════════════════════════════════════════

What sources document this moment:
1. Source: _________________ Type: _______ Reliability: ___
   What it provides: __________________________________
2. Source: _________________ Type: _______ Reliability: ___
   What it provides: __________________________________

═══════════════════════════════════════════════════════════
SCENE ELEMENTS CHECKLIST
═══════════════════════════════════════════════════════════

SETTING:
Physical location description:
[ ] DOCUMENTED: Source: _______________________________
[ ] INFERRED: From: __________________________________
[ ] RESEARCHED: Period sources for typical: ___________
[ ] INVENTED: □ PROHIBITED unless clearly marked

Weather/time of day:
[ ] DOCUMENTED: Source: _______________________________
[ ] INFERRED: Reasonable for date/location
[ ] INVENTED: □ USE SPARINGLY, don't over-specify

DIALOGUE:
[ ] DIRECT QUOTE: Source: _____________________________
[ ] PARAPHRASE of documented speech: Source: __________
[ ] RECONSTRUCTED from written accounts: Source: ______
[ ] INVENTED: □ PROHIBITED

ACTION:
Physical actions described:
[ ] DOCUMENTED: Source: _______________________________
[ ] INFERRED: From documented outcome
[ ] PLAUSIBLE: Based on known patterns
Note any inference in text: [ ] Yes [ ] N/A

SENSORY DETAIL:
Each sensory detail must be:
[ ] Documented
[ ] Researched (period-appropriate)
[ ] Explicitly qualified ("might have smelled...")
□ NOT invented specifically

═══════════════════════════════════════════════════════════
INTERIORITY LIMITS
═══════════════════════════════════════════════════════════

Internal states claimed in scene:

1. Claimed state: ____________________________________
   [ ] DOCUMENTED: Subject stated this feeling
       Source: ______________________________________
   [ ] INFERRED: From documented behavior/writing
       Basis: _______________________________________
       Marked as inference: [ ] Yes
   [ ] SPECULATIVE: □ REQUIRES explicit hedging
       Hedge language used: __________________________

PROHIBITED internal claims (never use unless quoted):
□ Specific thoughts ("He thought, 'X'")
□ Sensory experience ("She felt the cold")
□ Unwitnessed private emotion
□ Dreams or imaginings

═══════════════════════════════════════════════════════════
FINAL CHECK
═══════════════════════════════════════════════════════════

[ ] Every element has documented basis or qualified language
[ ] No prohibited interiority
[ ] Scene purpose served without overreach
[ ] Reader can distinguish documented from reconstructed
[ ] Endnote/footnote explains scene construction if needed
```

### 6.2 Interiority Rules

**What you CAN claim about internal states:**

| Claim Type | Source Required | Example |
|------------|-----------------|---------|
| Subject stated feeling | Direct quote/paraphrase | "She later wrote that she felt betrayed" |
| Contemporaries observed | Witness accounts | "Friends noted he seemed despondent" |
| Behavior indicates | Documented actions | "His abrupt departure suggests discomfort" |
| Pattern suggests | Multiple instances | "Given his consistent anxiety about X, he likely felt..." |

**What you CANNOT claim:**

- Specific thoughts not documented
- Emotions in private moments without witnesses
- Sensory experiences ("felt the warmth")
- Internal monologue
- Dreams, imaginings, fantasies
- Motivations without evidence

**Language for necessary inference:**

- "He may have felt..."
- "One imagines she was..."
- "He likely experienced..."
- "We cannot know what she thought, but..."
- "His behavior suggests..."

### 6.3 Sensory Detail Constraints

**Permitted sensory details:**

| Type | Documented | Period-Researched | Invented |
|------|------------|-------------------|----------|
| Visual (setting) | ✓ Preferred | ✓ With care | ✗ No |
| Visual (people) | ✓ Preferred | ✗ No | ✗ No |
| Sound | ✓ Preferred | ✓ Generic only | ✗ No |
| Smell | ✓ Preferred | ✓ Generic only | ✗ No |
| Touch/Temperature | ✓ If documented | ✗ Risky | ✗ No |
| Taste | ✓ If documented | ✗ No | ✗ No |

**Period research standard:**
- Must cite source for period-typical details
- "Streets would have been muddy" requires evidence of street conditions
- Generic ("the usual noise of the city") safer than specific

### 6.4 Structure Playbook

#### Three-Act Biography Structure

```
ACT I: FORMATION (typically 20-30% of book)
Purpose: Establish who subject becomes from
- Origins: Family, place, class, era
- Early influences: Education, mentors, experiences
- Inciting circumstances: What sets trajectory
- Early identity: Who were they before becoming known?

Key chapters might include:
1. Opening hook (scene that captures essence)
2. Origins and family
3. Childhood and education
4. Early career/calling
5. First significant achievement/failure

Throughline to establish: ______________________________

ACT II: ACHIEVEMENT/CONFLICT (typically 50-60% of book)
Purpose: The life's main work and struggles
- Rise: Key achievements, recognition
- Conflicts: Opposition, setbacks, controversies
- Relationships: Key figures in subject's life
- Evolution: How subject changes

Structural options:
[ ] Chronological progression
[ ] Thematic chapters (work, family, public life)
[ ] Interwoven chronological and thematic
[ ] Parallel narratives (subject + context)

Key chapters might include:
- Major work/achievement chapters
- Key relationship chapters
- Crisis/turning point chapters
- Public life vs private life chapters

Central conflict: ____________________________________

ACT III: LEGACY/RESOLUTION (typically 15-25% of book)
Purpose: Meaning and aftermath
- Late period: Final years, late work
- Death: Circumstances if relevant
- Immediate aftermath: Reception, response
- Legacy: What endures, what subject means
- Historiographical note: How views have changed

Key chapters might include:
- Late period chapter
- Death and immediate legacy
- Longer legacy/meaning
- Epilogue if needed

Final argument: ______________________________________
```

#### Chapter Outline Template

**See template file: `templates/chapter_outline.md`**

### 6.5 Pacing Guidelines

**Scene-to-Summary Ratio:**
- High drama moments: More scene, less summary
- Transitional periods: More summary, less scene
- Thematic chapters: Balanced
- Never more than 3 pages of pure summary without scene break

**Pacing by life period:**
| Period | Typical Pacing | Notes |
|--------|---------------|-------|
| Childhood | Medium-fast | Limited sources often; don't overstretch |
| Early career | Medium | Establish patterns, don't belabor |
| Peak achievement | Slower | Richest material; take time |
| Controversies | Slow | Careful, detailed treatment |
| Decline | Medium-fast | Don't wallow unless essential |
| Death | Varies | Match to death's significance |

**Chapter length guidelines:**
- Target consistency: ±20% of average chapter length
- Variation for emphasis is acceptable but intentional
- Short chapters increase pace
- Long chapters slow pace, allow depth

### 6.6 Recurring Motifs

```
MOTIF TRACKING SHEET

Motif 1: ____________________________________________
First appearance: Chapter ___ , Page ___
Recurrences:
- Chapter ___ , Page ___ : Context: __________________
- Chapter ___ , Page ___ : Context: __________________
- Chapter ___ , Page ___ : Context: __________________
Final appearance: Chapter ___ , Page ___
Evolution/meaning: ___________________________________

Motif 2: ____________________________________________
(Continue as needed)

MOTIF INVENTORY:
[ ] Physical object: _________________________________
[ ] Location: ________________________________________
[ ] Phrase/saying: ___________________________________
[ ] Relationship pattern: _____________________________
[ ] Theme: __________________________________________

Cross-check: Do motifs emerge from evidence or are they imposed?
Motifs grounded in sources: __________________________
Motifs that need stronger grounding: _________________
```

### 6.7 Character Network Mapping

```
CHARACTER NETWORK MAP

PRIMARY CHARACTERS (substantial presence):
┌─────────────────────────────────────────────────────────────┐
│ Name: ________________________________________________      │
│ Relationship to subject: _______________________________    │
│ Period in subject's life: ______________________________    │
│ Role in narrative: ____________________________________     │
│ Sources for this person: _______________________________    │
│ Chapter appearances: ___________________________________    │
│ Arc: __________________________________________________     │
└─────────────────────────────────────────────────────────────┘
(Repeat for each primary character, typically 5-10)

SECONDARY CHARACTERS (recurring):
┌─────────────────────────────────────────────────────────────┐
│ Name: _________________ Relation: ______ Chapters: _______  │
│ Brief description: _____________________________________    │
└─────────────────────────────────────────────────────────────┘
(Typically 10-25 secondary characters)

MINOR CHARACTERS (brief appearances):
(List names and single-line identification)

CHARACTER INTRODUCTION TRACKING:
[ ] Each character introduced with identifying context
[ ] No character introduced then dropped without resolution
[ ] Important characters reintroduced if gap between appearances
[ ] Reader can track who is who

RELATIONSHIP MAP:
(Diagram key relationships)

          [Subject]
         /    |    \
   [Family]  [Work]  [Personal]
      |        |         |
   [Name]   [Name]    [Name]
```

### 6.8 Balancing Scholarship and Storytelling

**Techniques for Integration:**

| Scholarly Need | Storytelling Solution |
|----------------|----------------------|
| Citation-heavy claim | Front-load narrative, footnote evidence |
| Historiographical debate | Scene first, then "Historians have debated..." |
| Complex context | Integrate into character experience |
| Uncertainty acknowledgment | Weave into narrative ("What happened next is unclear...") |
| Technical/specialized content | Anchor in human moment |
| Source discussion | Move to notes unless dramatizable |

**What to keep in text vs notes:**

| In Main Text | In Notes |
|--------------|----------|
| Essential evidence | Source details |
| Key quotes | Extended quotations |
| Necessary hedging | Methodological discussion |
| Significant debates | Scholarly apparatus |
| Subject's own words | Historiographical context |
| Narrative momentum | Technical discussions |

**Language register:**
- Avoid academic jargon in main text
- Define necessary terms on first use
- Prefer concrete over abstract
- Active voice over passive
- Specific over general

---

## Module 7: Templates

All templates are provided as separate files in the `templates/` directory:

1. `templates/source_intake_form.md` - For documenting each source
2. `templates/claim_ledger_entry.md` - For tracking individual claims
3. `templates/chapter_outline.md` - For planning chapters
4. `templates/verification_checklist.md` - For fact-checking process

---

## Module 8: Production Stages and Quality Gates

### 8.1 Staged Production Plan

```
═══════════════════════════════════════════════════════════════════
STAGE 1: RESEARCH
═══════════════════════════════════════════════════════════════════

Objective: Build comprehensive, organized evidentiary foundation

Tasks:
□ Complete Question Framing Worksheet
□ Execute Source Discovery Protocol
□ Complete Source Intake for all sources
□ Build initial Source Map
□ Begin Claim Ledger (research-phase claims)
□ Conduct preliminary interviews
□ Identify gaps and plan gap-filling

Deliverables:
- Completed Question Framing Worksheet
- Source database with all sources processed
- Initial Source Map
- Research memo identifying key findings and gaps
- Preliminary chapter structure

Quality Gate 1 criteria: See Gate 1 below

═══════════════════════════════════════════════════════════════════
STAGE 2: DRAFTING
═══════════════════════════════════════════════════════════════════

Objective: Transform research into narrative manuscript

Tasks:
□ Finalize chapter outline
□ Draft each chapter
□ Apply Scene Construction Protocol for all scenes
□ Maintain Claim Ledger (add claims as written)
□ Track character introductions
□ Implement motif structure
□ Write front matter (introduction, preface)
□ Write end matter (epilogue, afterword)

Deliverables:
- Complete draft manuscript
- Claim Ledger populated for all claims
- Updated Source Map (chapter-level)
- Character network documentation

Quality Gate 2 criteria: See Gate 2 below

═══════════════════════════════════════════════════════════════════
STAGE 3: VERIFICATION
═══════════════════════════════════════════════════════════════════

Objective: Ensure every claim is properly supported and accurate

Tasks:
□ Run verification protocols (dates, names, locations, quotes)
□ Check all claims against Claim Ledger requirements
□ Execute Red Team Pass
□ Resolve all contradictions
□ Update confidence levels
□ Fact-check with independent checker if possible
□ Legal review if needed (defamation, privacy)

Deliverables:
- Verification checklist completed for each chapter
- Red Team report
- Updated Claim Ledger with verification status
- Legal review memo (if applicable)

Quality Gate 3 criteria: See Gate 3 below

═══════════════════════════════════════════════════════════════════
STAGE 4: REVISION
═══════════════════════════════════════════════════════════════════

Objective: Improve narrative quality and address all verification issues

Tasks:
□ Revise based on verification findings
□ Complete Bias Audit
□ Complete Missing Voices Review
□ Conduct pacing review
□ Check scene-to-summary balance
□ Verify motif consistency
□ Review character clarity
□ Ensure hedging language consistency
□ Beta reader feedback round
□ Structural revision if needed

Deliverables:
- Revised manuscript
- Completed Bias Audit
- Beta reader feedback summary
- Revision tracking document

Quality Gate 4 criteria: See Gate 4 below

═══════════════════════════════════════════════════════════════════
STAGE 5: COPYEDIT
═══════════════════════════════════════════════════════════════════

Objective: Polish prose and ensure consistency

Tasks:
□ Professional copyedit
□ Citation format check
□ Quotation accuracy final check
□ Name/date consistency check
□ House style compliance
□ Front/back matter formatting
□ Notes formatting

Deliverables:
- Copyedited manuscript
- Style sheet
- Citation check report

Quality Gate 5 criteria: See Gate 5 below

═══════════════════════════════════════════════════════════════════
FINAL: MANUSCRIPT DELIVERY
═══════════════════════════════════════════════════════════════════

Deliverables:
- Final manuscript files
- Complete notes/bibliography
- Source archive (organized)
- Claim Ledger (final)
- Image/illustration files with permissions
- Index entries (if applicable)
```

### 8.2 Quality Gates

**See detailed criteria file: `quality_gates.md`**

---

## Appendix A: Controlled Vocabularies

### Source Type Codes
- DOC: Document (letters, memos, manuscripts)
- INT: Interview (conducted for this project)
- PUB: Publication (books, articles)
- GOV: Government record
- IMG: Image (photographs, artwork)
- AUD: Audio recording
- VID: Video recording
- OBJ: Physical object
- WEB: Web source
- ORA: Oral history (archival)

### Claim Type Codes
- F: Fact
- I: Interpretation
- C: Context
- Q: Quotation
- S: Scene

### Confidence Codes
- V: Verified
- P: Probable
- CT: Contested
- SP: Speculative
- U: Unknown

### Uncertainty Codes
- UNK: Unknown
- AMB: Ambiguous
- CON: Contested
- PRB: Probable
- SPC: Speculative

---

## Appendix B: Quick Reference Cards

### The Ten Commandments of Biographical Evidence

1. **No claim without source** (or explicit acknowledgment of gap)
2. **Primary over secondary** when available
3. **Multiple over single** for contested claims
4. **Contemporary over retrospective** for facts
5. **Document over memory** when they conflict
6. **Verify, then trust** all quotations
7. **Hedge honestly** rather than overstate
8. **Acknowledge opposition** rather than suppress
9. **Context before judgment** always
10. **Transparency over authority** in all disputes

### Scene Construction Quick Check

Before any scene, answer:
1. What source documents this moment? ___
2. Can I quote dialogue or must I paraphrase? ___
3. What sensory details are documented vs. researched? ___
4. Am I claiming internal states? If so, sourced how? ___
5. Would another biographer agree this is fair? ___

### Uncertainty Quick Guide

| If evidence is... | Your confidence is... | Your language is... |
|-------------------|----------------------|---------------------|
| Multiple, independent, clear | VERIFIED | State as fact |
| Single but reliable | PROBABLE | Minimal hedging |
| Conflicting | CONTESTED | Present multiple views |
| Inferential | SPECULATIVE | Clear hedging |
| Absent | UNKNOWN | Acknowledge or omit |

---

*System Version 1.0*
*For use with all biography projects requiring academic rigor and narrative engagement*
