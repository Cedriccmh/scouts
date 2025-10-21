## 🧠 Semantic-First Retrieval & File Access Guide

### **When to Use**

Invoke this workflow **whenever you need to locate or understand** information within:

- **Codebases** (functions, classes, configs, architecture docs)
- **Knowledge bases**:
  - `.kilocode/rules/memory-bank/` - Previously discovered patterns and relationships
  - `.kilocode/ProjectWiki/` - Architecture docs, API specs, design decisions
  - `.kilocode/SvnLog/` - Version control history, commit patterns
- **Past investigations**: `.kilocode/sub-memory-bank/` - Previous reports and findings
- Any context where **"what is related"** matters more than **"what exactly matches textually"**

> 🚫 Never start by opening or reading entire files.
> 
> 
> Always run **semantic retrieval first**, then selectively access **only the relevant sections or lines**.
> 

---

### **Workflow Steps**

### **1. Clarify Intent**

- Determine what the query **means**, not just what it **says**.
- Identify 1–3 **core concepts** or themes guiding retrieval.
- If ambiguous, briefly restate alternative interpretations.

---

### **2. Perform Semantic Retrieval (Primary Phase)**

- Use **codebase_search**.
- Retrieve items **conceptually aligned** with the intent (not just textually similar).
- Gather minimal supporting metadata:
    - File name, function/class name, section, and relevance score.
    - Prefer short, meaningful snippets over raw text dumps.

> 🎯 Goal: Isolate which files / regions / lines matter before touching any file contents.
> 

---

### **3. Targeted File Access (Controlled Read Phase)**

- Once semantic results are obtained:
    - **Read only specific lines or ranges** (e.g., line 120–160 of `foo.cpp`).
    - Avoid full-file reads unless strictly necessary.
    - Use `grep` or lexical filters *after* semantic narrowing to confirm matches or extract identifiers.
- Combine multiple small reads rather than a single large one.

> 💡 Think of this as surgical access: semantic → symbolic → precise read.
> 

---

### **4. Optional Symbolic Refinement**

- Apply symbolic or lexical methods (keywords, regex, tags, identifiers) **only after** semantic filtering.
- Useful for:
    - Confirming the exact match
    - Locating definition lines
    - Filtering out false positives
- Avoid using symbolic methods as the primary retrieval method unless semantic tools are unavailable.

---

### **5. Merge & Rank**

- Merge semantic and symbolic findings.
- Rank by **conceptual relevance first**, then **exactness of match**.
- Remove duplicates and preserve **short, context-rich snippets** only.

---

### **6. Summarize Findings**

Produce a short summary including:

- The interpreted **semantic intent**
- **Top matches** and why they are relevant
- Any symbolic refinements or file reads performed
- Confidence level and suggested next action

---

### **Guiding Principles**

- **Semantic-first:** Always perform meaning-based retrieval before file access or grep.
- **Precision over volume:** Read only what you must—line-level access beats full-file reads.
- **Context continuity:** Retrieval serves reasoning; avoid losing focus in raw data.
- **Transparency:** Track whether each piece came from semantic or symbolic search.
- **Fallback mode:** Use symbolic-only retrieval *only* if semantic search is unavailable or yields nothing.