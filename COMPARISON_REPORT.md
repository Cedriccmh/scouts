# Scouts Fork Divergence Analysis

**Comparison between**: [Cedriccmh/scouts](https://github.com/Cedriccmh/scouts) (fork) vs [TokenRollAI/cc-plugin](https://github.com/TokenRollAI/cc-plugin) (original)

**Date**: October 22, 2025

---

## TL;DR - Critical Issues

### 🚨 What the Fork REMOVED:
2. **"Zero subjective judgments" rule** - Weakened objectivity guarantees
3. **Descriptive file naming** - Date-prefix format less informative
4. **Flexible tool usage** - Forced to use semantic-first even when inappropriate

### ⚠️ What the Fork ADDED (Questionable Value):
5. **Mandatory semantic-first** - Slower for simple exact-match queries
7. **Formalized iteration boundaries** - "20% incremental value" is subjective/unmeasurable
8. **Quality checklist** - No enforcement, just overhead

---

## 1. What the Original Has That the Fork Removed

### 1.3 No Content Duplication Rule (REMOVED)

**Original** mandates:
- "Ensure zero overlap between different documents"
- "Each piece of information should appear in exactly one document"
- Clear guidance on handling cross-document relevance

**Fork**: No mention of content duplication control

**Impact**: ❌ Potential for redundant information across multiple reports

### 1.4 Descriptive Multi-Word File Naming (REMOVED)

**Original** enforces:
- "MUST use multiple words separated by hyphens"
- Good examples: `how-to-add-api-in-backend-server.md`, `trpc-router-architecture-analysis.md`
- Bad examples: `api.md`, `auth.md`, `analysis.md`

**Fork**: Uses date-prefix format `yy-mm-dd-target.md` where "target" is just a "concise description"

**Impact**: ❌ Less descriptive file names, harder to understand content from file name alone

### 1.5 Strict 200-Line Limit (RELAXED)

**Original**: 
- "HARD LIMIT: Maximum 200 lines per document"
- "Longer is NOT better - focus on relevant, non-redundant information"

**Fork**: Increased to 300 lines

**Impact**: ⚠️ Potential for longer, less focused reports

---

## 2. What the Original Has in withScout That the Fork Removed


## 3. Unnecessary Complexity Added in the Fork


### 3.2 Step 0: Memory Bank Pre-Check (Premature Optimization)

**Fork adds entire pre-investigation phase**:
1. Read Memory Bank Index
2. Extract relevant pointers
3. Review specific past reports
4. Prepare structured "Known Information" for scouts

**Problems**:
- ❌ Adds overhead to every investigation
- ❌ Assumes index exists and is up-to-date
- ❌ Coordinator (withScout) becomes a bottleneck
- ❌ **Original's direct approach was faster for first-time investigations**

### 3.6 Incremental Report Writing (Complexity Workaround)

**Fork mandates**:
- "Write the document in batches (append mode)"
- "First: Metadata & Code Sections"
- "Second: Conclusions & Relations"
- "Third: Result & Attention"
- "NEVER attempt to write everything in a single operation!"

**Why this exists**: Working around 300-line report bloat

**Problems**:
- ❌ More tool calls = slower execution
- ❌ Risk of incomplete reports if process interrupted
- ❌ **Original's 200-line limit allowed single-write reports**

### 3.7 Quality Control Checklist (Bureaucracy)

**Fork adds 5-point quality checklist**:
- Every code section must have file path and line numbers
- 70% of research questions answered
- All findings linked to source
- Relations section shows dependencies
- Attention section highlights risks

**Problems**:
- ❌ No clear enforcement mechanism
- ❌ Subjective "70%" threshold
- ❌ Adds overhead without guaranteed quality improvement
- ❌ **Original's "zero subjective judgments" rule was simpler and more effective**

### 3.8 Iteration Boundaries (Formalized Inefficiency)

**Fork formalizes**:
- Maximum 3 rounds
- 20% incremental value threshold
- Convergence checks

**Problems**:
- ❌ How do you measure "20% new actionable information"?
- ❌ Artificial limits may stop before completion
- ❌ Adds calculation overhead
- ❌ **Original's flexible iteration worked based on actual need**


### 3.10 6-Section Report Template (Template Bloat)

**Fork requires**:
1. Investigation Summary (with Task Type Rationale, Search Scopes, etc.)
2. Key Findings (subdivided by scout)
3. Cross-Area Connections
4. Knowledge Gaps & Uncertainties
5. Actionable Recommendations
6. Appendix (Scout Deployment History, Evidence Trail)

**Original**: 
- Evidence Section
- Findings Section
- Done.

**Problems**:
- ❌ Creates long, bureaucratic reports
- ❌ Forces structure even when not needed
- ❌ "Knowledge Gaps" section documents what you *don't* know
- ❌ **Original's 2-section format was cleaner and more focused**

---

## 4. Critical Regression Summary

| Feature | Original | Fork | Assessment |
|---------|----------|------|------------|
| **Action Phase** | ✅ Implements/fixes/documents | ❌ Only generates reports | 🚨 **CRITICAL LOSS** |
| **Workflow** | 6 steps, ends with implementation | 5 steps (+ Step 0), ends with report | ❌ Regression |
| **File Naming** | Descriptive multi-word | Date-prefix + vague description | ❌ Less usable |
| **Report Length** | 200 lines max | 300 lines max | ⚠️ Encourages bloat |
| **Tool Flexibility** | Any tool as needed | Forced semantic-first | ❌ Less flexible |
| **Objectivity** | Strong "zero subjective judgments" | Weakened emphasis | ❌ Quality risk |
| **Simplicity** | Simple workflow | Complex infrastructure | ❌ Higher barrier to entry |
| **Content Duplication** | Explicitly prohibited | No control | ❌ Quality risk |
| **Use-Case Examples** | Concrete examples provided | Abstract descriptions | ❌ Less clear |

---

## 5. When Each Version Makes Sense

### Use **Original (TokenRollAI/cc-plugin)** when:

✅ **You want to actually implement features** (not just document them)
✅ You need quick, actionable intelligence
✅ You want objective, fact-based reports
✅ You prefer simple, clear workflows
✅ You're working alone or in small teams
✅ You value execution over documentation
✅ Your codebase is small-to-medium size
✅ You want something that "just works"

### Use **Fork (Cedriccmh/scouts)** when:

⚠️ You only need investigation reports (no implementation)
⚠️ You have time to set up Memory Bank infrastructure
⚠️ You have existing ProjectWiki and SvnLog directories
⚠️ You can maintain index files manually
⚠️ You're building a long-term knowledge base
⚠️ You're willing to trade simplicity for formalization
⚠️ You have semantic search infrastructure available
⚠️ You value process over results

---

## 6. Conclusion

### The Fundamental Trade-off

The fork **sacrifices practical utility for architectural purity**:

- **Lost**: Action/implementation phase, simplicity, flexibility, clear examples
- **Gained**: Complex infrastructure, formalized processes, bureaucratic overhead

### Critical Finding

**The fork removed the ability to actually do work.** 

The original's workflow:
```
Research → Implement → Done
```

The fork's workflow:
```
Pre-check → Research → Report → Stop
```

### Recommendation

**For most users, the original (TokenRollAI/cc-plugin) is superior** because:

1. ✅ It actually completes tasks (implements features, fixes bugs)
2. ✅ Simpler to use (4 steps vs. 8 steps + Step 0)
3. ✅ More flexible tool usage
4. ✅ Stronger objectivity guarantees
5. ✅ Clearer documentation with concrete examples
6. ✅ No infrastructure setup required
7. ✅ More focused reports (200 lines vs. 300 lines)

**The fork may be valuable only if**:
- You already have a Memory Bank infrastructure
- You genuinely need investigation-only workflow (no implementation)
- You're building an enterprise knowledge base
- You have dedicated personnel to maintain indices

### Final Verdict

**Choose the original unless you have a specific reason to choose the fork.**

The fork's architectural complexity is **not justified** for most use cases, and the removal of the implementation phase is a **critical regression** that makes the plugin incomplete.

---

## Appendix: Summary Table

| Category | What Was Lost | What Was Added (Unnecessarily) |
|----------|---------------|-------------------------------|
| **Core Function** | ❌ Action/Implementation phase | ➕ Investigation-only workflow |
| **Workflow** | ❌ Simple 6-step process | ➕ 8-step process + Step 0 pre-check |
| **Documentation** | ❌ Clear use-case examples | ➕ Abstract descriptions |
| | ❌ "Zero subjective judgments" emphasis | ➕ Quality checklist (unenforced) |
| | ❌ Descriptive file names | ➕ Date-prefix names |
| | ❌ 200-line limit | ➕ 300-line reports |
| | ❌ No content duplication rule | ➕ 6-section template |
| **Infrastructure** | ❌ Simple `llmdoc/` structure | ➕ Complex `.kilocode/` ecosystem |
| | | ➕ Memory Bank Index (manual maintenance) |
| | | ➕ ProjectWiki/SvnLog assumptions |
| **Search** | ❌ Flexible tool usage | ➕ Mandatory semantic-first |
| | | ➕ Search domain specification |
| | | ➕ Task type classification |
| **Process** | ❌ Flexible iteration | ➕ Formalized boundaries (3 rounds, 20% threshold) |
| | | ➕ Responsibility boundaries table |
| | | ➕ Incremental report writing |

---

**Report Generated**: October 22, 2025  
**Analysis Type**: Regression and Complexity Analysis  
**Comparison Scope**: `agents/scout.md` and `commands/withScout.md`  
**Key Finding**: Fork removed implementation capability and added unnecessary architectural complexity

**Repositories**:
- ✅ **Original (Recommended)**: https://github.com/TokenRollAI/cc-plugin (151 stars)
- ⚠️ **Fork (Use with caution)**: https://github.com/Cedriccmh/scouts (0 stars, forked from cc-plugin)

