---
description: Use the scout agent to gather information, then read the collected data, organize and classify it, and finally output a comprehensive report.
---

This command is designed to tackle complex tasks through a structured exploration framework. It emphasizes meticulous **planning** before action, efficient information gathering via **parallel** `scout` agents, and a gradual approach to the final solution through **iteration**.

> **Important**: When the `/withScout` command is enabled, the system operates as an **information retrieval engine**. The primary output is a comprehensive **investigation report**, not direct code implementation or execution.

### Core Philosophy

1.  **Plan Before You Act**: Before launching any scout, the primary, often ambiguous, goal must be broken down into a set of clear, independently investigable questions.
2.  **Divide and Conquer**: For complex systems, deploying multiple `scout` agents (2-3 maximum) simultaneously, each with a distinct and independent area of responsibility, dramatically increases the efficiency and breadth of information gathering.
3.  **Iterative Convergence**: Accept that a single round of scouting may not solve the entire problem. Each subsequent round should build upon the last, asking more precise and deeper questions to progressively narrow the scope of the unknown and converge on an executable solution.

**Iteration Boundaries**:

- **Maximum Iterations**: Limit scouting to **3 rounds maximum** for most tasks to prevent diminishing returns.
- **Convergence Check**: After each round, evaluate whether new findings are substantial enough to justify another iteration.
- **Incremental Value**: Each iteration should add significant new knowledge. If Round N adds less than 20% new actionable information compared to Round N-1, consider concluding the investigation with current findings.
- **Document Limitations**: If gaps remain after reaching iteration limits, clearly document them in the final report's "Knowledge Gaps & Uncertainties" section.

---

### Workflow

#### Step 0: Memory Bank Pre-Check (Lightweight Index-Based)

Before starting a new investigation, perform a lightweight knowledge check. **Stay at the index level—let scouts do the deep diving.**

1.  **Read Memory Bank Index** (Central Hub):
    - Read `<project-root>/.kilocode/rules/memory-bank/index.md` if it exists
    - This index contains:
      * Previously discovered module relationships
      * Known architectural patterns and component interactions
      * **Pointers** to relevant ProjectWiki docs and SvnLog entries
      * Links to past investigation reports
      * Known system diagrams and dependency graphs
    - **Do NOT browse ProjectWiki or SvnLog directly** at this stage—extract pointers only

2.  **Extract Relevant Pointers from Index**:
    - Identify which past investigations are related to the current task
    - Note which ProjectWiki docs the index suggests are relevant (file paths only, don't read yet)
    - Note which SvnLog time periods/commits the index highlights (references only, don't browse yet)
    - Identify known module relationships that might be relevant
    - List areas the index marks as well-documented vs. knowledge gaps

3.  **Review Specific Past Reports** (if index points to them):
    - Only read reports from `.kilocode/sub-memory-bank/report/` that index explicitly references as relevant
    - Extract key findings and known patterns from these reports
    - Note any evolving areas that need re-investigation

4.  **Prepare Structured Context for Scouts**:
    - Compile "Known Information" with clear structure (see template below)
    - Provide index-derived pointers (not full content) to scouts
    - List well-documented areas to de-prioritize
    - List knowledge gaps to prioritize
    - Avoid duplicating work scouts will do—just provide navigation hints

> **Key Principle**: You are a planner, not an investigator. Read the index, extract pointers, and let scouts do the deep exploration into ProjectWiki, SvnLog, and code based on your guidance.

> **Note**: If this is the first investigation in the project, the index won't exist. That's expected—proceed to Step 1 with empty "Known Information".

#### Step 1: Deconstruction & Planning

This is the most critical step in the entire process. First, deeply understand the user's end goal, then break it down.

1.  **Define the Ultimate Goal & Identify Task Type**:
    - Clarify what the user wants to accomplish (e.g., "Implement a JWT token refresh feature")
    - **Identify Task Type** to guide search strategy and data source prioritization:
      * **Bug/Debug**: Focus scouts on call chains, recent changes, execution flow analysis
        - **Prioritize**: SvnLog (recent commits, bug fix patterns), error traces, test cases
        - **Search**: Recent modifications, historical similar issues, author contexts
      * **Feature Development**: Direct scouts to API interfaces, module boundaries, architectural documentation
        - **Prioritize**: ProjectWiki (design docs, API specs), existing similar features, architecture diagrams
        - **Search**: Interface definitions, integration patterns, design decisions
      * **Refactoring**: Point scouts to cross-module dependencies, coupling points, architectural patterns
        - **Prioritize**: SvnLog (code evolution history), ProjectWiki (original design intent), dependency graphs
        - **Search**: Architectural constraints, historical refactoring attempts, coupling analysis
    - This task type will inform each scout's search approach and domain selection

2.  **Deconstruct into Research Areas**: Break the goal down into several key areas that require separate investigation.
    - Area A: Authentication state management and API call logic in the frontend codebase.
    - Area B: Authentication middleware, routes, and token generation/validation logic in the backend codebase.
3.  **Assign Scouts to Each Area**: Assign a `scout` agent to each research area and define its **independent responsibilities**.
    - `Scout A (Frontend)`: Responsible for analyzing the client-side code.
    - `Scout B (Backend)`: Responsible for analyzing the server-side code.
4.  **Formulate Initial Research Questions**: Design a set of highly specific, targeted questions for each `scout`.

#### Step 2: Parallel Scout Deployment

Use the `Task` tool to launch multiple `scout` agents **concurrently**. Use the following template to ensure tasks are independent and comprehensive.

**Parallel Scout Task Template**:

```
=== Global Context ===
Primary Goal: [Describe the overall task to be completed]
Task Type: [Bug/Debug | Feature Development | Refactoring]
Working Directory: [Provide the project root directory]

Known Information: [Structured context from Memory Bank index - provide navigation hints, not full content]
  Past Findings (from index):
    - [Specific finding from index, e.g., "Auth uses Redux for state management (see report/24-10-15-auth.md)"]
    - [Another finding, e.g., "Token validation happens in middleware/auth.js"]
  
  Relevant Documentation Pointers (from index):
    - [Index-suggested docs, e.g., "ProjectWiki/architecture/auth-flow.md covers token lifecycle"]
    - [Another pointer, e.g., "ProjectWiki/api/auth-endpoints.md has API specs"]
  
  Relevant History Pointers (from index):
    - [Index-suggested commits, e.g., "SvnLog: Auth refactored in 2024-09, commits r12345-r12350"]
    - [Another pointer, e.g., "SvnLog: Bug fix for token expiration in r11234"]
  
  Known Module Relationships (from index):
    - [e.g., "Frontend auth module → Backend /api/auth → AuthService → Database"]
  
  Known Gaps (from index):
    - [What index shows is missing, e.g., "No documented refresh token mechanism"]
    - [Another gap, e.g., "Token expiration strategy not documented"]
  
  De-prioritize (well-documented areas from index):
    - [e.g., "Login flow fully documented in report/24-08-20-login.md, focus on refresh instead"]

=== Scout A: [Role name, e.g., Frontend Auth Investigator] ===
Responsibility: [Define Scout A's scope, e.g., Investigate auth patterns and token handling in the frontend codebase]

Search Scope:
  - Directories: [e.g., frontend/src/auth/, frontend/src/api/]
  - File Types: [e.g., .ts, .tsx, .js] (optional - scouts can auto-detect)
  - Domains: [Select from: codebase / ProjectWiki / SvnLog / documentation / multiple]
    * codebase: Source code files and configuration
    * ProjectWiki: Architecture docs (.kilocode/ProjectWiki/), design specs, API documentation
    * SvnLog: Version control history (.kilocode/SvnLog/), commit messages, change patterns
    * documentation: All docs (ProjectWiki + inline comments + README files)
    * multiple: Combine multiple domains (e.g., "codebase + ProjectWiki")

Research Questions (phrase as natural language for semantic search):
1. [Question 1, e.g., How does the application store JWT tokens after user login?]
2. [Question 2, e.g., Where are authentication headers injected into API requests?]
3. [Question 3, e.g., Is there a global interceptor for handling 401/403 authentication errors?]

Expected Deliverables:
  - Report Location: <project-root>/.kilocode/sub-memory-bank/scout/yy-mm-dd-frontend-auth.md
  - Key Focus: Token storage mechanism, API interceptor logic, error handling flow

=== Scout B: [Role name, e.g., Backend API Investigator] ===
Responsibility: [Define Scout B's scope, e.g., Investigate the authentication mechanism of the backend API]

Search Scope:
  - Directories: [e.g., backend/auth/, backend/middleware/]
  - File Types: [e.g., .py, .js, .ts]
  - Domains: [Select from: codebase / ProjectWiki / SvnLog / documentation / multiple]
    * codebase: Source code files and configuration
    * ProjectWiki: Architecture docs (.kilocode/ProjectWiki/), design specs, API documentation
    * SvnLog: Version control history (.kilocode/SvnLog/), commit messages, change patterns
    * documentation: All docs (ProjectWiki + inline comments + README files)
    * multiple: Combine multiple domains (e.g., "codebase + SvnLog" for bug investigations)

Research Questions:
1. [Question 1, e.g., Which middleware validates incoming JWT tokens in API requests?]
2. [Question 2, e.g., What are the current endpoints for user authentication and token management?]
3. [Question 3, e.g., How is the JWT token payload structured and where is expiration configured?]

Expected Deliverables:
  - Report Location: <project-root>/.kilocode/sub-memory-bank/scout/yy-mm-dd-backend-auth.md
  - Key Focus: Middleware structure, authentication endpoints, token configuration

...
```

**Note**: It is recommended to keep the number of parallel scouts at 2-3 to avoid excessive management overhead and information overload.

**Responsibility Boundaries**:

To ensure clear division of labor between the coordinator (withScout) and scouts:

| Activity | withScout Responsibility | Scout Responsibility |
|----------|-------------------------|---------------------|
| **Read Memory Bank Index** | ✅ Lightweight read, extract pointers | ⚠️ Only if Known Info insufficient |
| **Browse ProjectWiki** | ❌ Don't browse directly | ✅ On-demand load (guided by pointers) |
| **Browse SvnLog** | ❌ Don't browse directly | ✅ On-demand load (guided by pointers) |
| **Read Past Reports** | ✅ Read index-referenced reports | ✅ Read task-related scout reports |
| **Semantic Code Search** | ❌ Don't search directly | ✅ Core responsibility |
| **Prepare Known Info** | ✅ Structure navigation hints | ❌ Receive and use hints |
| **Report Integration** | ✅ Integrate all scout reports | ❌ Generate single report only |
| **Task Decomposition** | ✅ Break down and assign | ❌ Execute assigned tasks |

> **Key Principle**: withScout is the **planner** (reads index, provides navigation), scouts are the **investigators** (follow pointers, do deep exploration).

#### Step 3: Synthesize & Evaluate

Once all `scout` agents have completed their tasks, consolidate their findings.

**Report Integration Process**:

1.  **Read Scout Reports**: Access each scout's output from:
    - `<project-root>/.kilocode/sub-memory-bank/scout/yy-mm-dd-[scout-topic].md`
    - Review the Metadata, Code Sections, Conclusions, Relations, and Attention sections from each report

2.  **Integrate Reports**: Combine the reports from each scout to form a holistic view:
    - Merge all Code Sections into a unified list
    - Consolidate Conclusions from different areas
    - Aggregate all Attention items (uncertainties, conflicts, risks)

3.  **Identify Key Connections**: Cross-reference findings across scouts:
    - Match frontend calls to backend endpoints (e.g., `apiClient.login()` → `/api/auth/login`)
    - Trace data flow across modules (e.g., form submission → API layer → service layer → database)
    - Identify API contracts and interface definitions
    - **Build a textual relationship map** showing how different areas interact

4.  **Discover Knowledge Gaps or Conflicts**: 
    - Is the current information complete? (Check if all research questions were answered)
    - Are there contradictions between scout findings? (e.g., different token storage locations mentioned)
    - Have new, unexpected questions emerged that weren't in the original plan?

**Understanding Scout Report Format**:

Each scout generates a standardized report containing:
- **Metadata**: Investigation date, search scope, iteration rounds, search strategy, and original research questions
- **Code Sections**: All discovered code locations with precise line numbers (`path/file:start~end`)
- **Conclusions**: Key findings and important discoveries about the investigated area
- **Relations**: Cross-file dependencies, function-to-function calls, module-to-module interactions
- **Result**: Direct answers to the assigned research questions
- **Attention**: Potential problems, uncertainties, or conflicts (limited to <20 lines for focus)

This standardized structure enables efficient cross-scout synthesis and comparison.

**Quality Control Checklist**:

Before proceeding to the next step, verify the quality of scout outputs:

- ✅ **Completeness**: Each scout should answer at least **70% of assigned research questions** with specific evidence (file paths, code snippets, configurations).
- ✅ **Specificity**: Findings should contain concrete details, not vague descriptions. Example: "Token is stored in Redux at `state.auth.token` (see `src/store/authSlice.ts:45`)" ✓ vs "Token is stored somewhere" ✗
- ✅ **Evidence-Based**: Prioritize findings backed by actual code or documentation over assumptions. Clearly mark any assumptions or uncertainties.
- ✅ **Conflict Resolution**: When multiple scouts provide conflicting information:
  - Cross-reference with actual code to determine ground truth
  - Document the conflict and the resolution method
  - If unresolvable, mark as an uncertainty for the next iteration

**If Quality is Insufficient**:
- Refine the original research questions to be more specific
- Re-deploy scouts with clearer scopes and additional context
- Consider splitting overly broad questions into smaller, focused ones

#### Step 4: Iterate or Execute

This is a critical decision point. Ask yourself: **"Based on the information gathered, do we have a clear and complete blueprint to begin execution?"**

- **If the answer is "No" (Iterate)**:

  1.  Based on the knowledge gaps identified in the previous step, **formulate a new round of more specific, in-depth research questions**.
  2.  Return to **Step 2** and launch a new round of scouting. The goal of this cycle is to fill the gaps, bringing your understanding closer to an executable state. This loop can be repeated multiple times, with each iteration getting closer to the final goal.

- **If the answer is "Yes" (Execute)**:

  1.  You now have sufficient information. Proceed to the next step to summarize and report.

#### Step 5: Summarize & Report

When delivering the final result to the user, clearly explain the entire process.

1.  **Summary of Investigation**: Briefly explain how you used iterative scouting to understand the problem.
2.  **Key Findings**: Present the core discoveries from the `scout` agents.
3.  **Actions Taken**: Detail the specific steps you took based on those findings.
4.  **Final Outcome**: Show the final report.

**Report Persistence**:

- The final investigation report **must be saved** in Markdown format.
- **Location**: `<project-root>/.kilocode/sub-memory-bank/report/yy-mm-dd-topic.md`
  - Use the date format `yy-mm-dd` (e.g., `25-10-21` for October 21, 2025).
  - Replace `topic` with a concise, kebab-case description of the investigation subject (e.g., `jwt-refresh-implementation`).
  - **If the directory doesn't exist**: Create the full path `<project-root>/.kilocode/sub-memory-bank/report/` before saving.
- **Content**: Follow the standard report structure template (see below).

**Report Structure Template**:

```markdown
# [Topic Title]

**Date**: [YYYY-MM-DD]  
**Task Type**: [Bug/Debug | Feature Development | Refactoring]  
**Investigation Rounds**: [Number]  
**Total Scouts Deployed**: [Number]

## 1. Investigation Summary
- **Original Goal**: [User's initial request]
- **Task Type Rationale**: [Why this task type was chosen and how it influenced the approach]
- **Search Scopes**: [Summary of all directories/file types covered across all scouts]
- **Approach**: [How the problem was deconstructed and assigned to scouts]
- **Iterations**: [Brief overview of each scouting round and what each iteration discovered]

## 2. Key Findings

### From Scout A: [Role Name]
- **Responsibility**: [What this scout investigated]
- **Finding 1**: [Detailed discovery with file paths/line numbers if applicable]
- **Finding 2**: [...]
- **Finding N**: [...]

### From Scout B: [Role Name]
- **Responsibility**: [What this scout investigated]
- **Finding 1**: [...]
- **Finding 2**: [...]

[Repeat for each scout deployed]

## 3. Cross-Area Connections
- [How findings from different scouts relate to each other]
- [Integration points between different system components]
- [Dependencies discovered across areas]

## 4. Knowledge Gaps & Uncertainties
- [What remains unknown or requires further investigation]
- [Areas where information was conflicting or unclear]
- [Assumptions made due to incomplete data]

## 5. Actionable Recommendations
Based on the investigation, the following actions are recommended:
1. [Specific action with justification]
2. [Specific action with justification]
3. [...]

## 6. Appendix

### Scout Deployment History
**Round 1**:
- Scout A: [Questions asked]
- Scout B: [Questions asked]

**Round 2** (if applicable):
- Scout A: [Refined questions]
- Scout B: [Refined questions]

### Evidence Trail
- [Key file paths examined]
- [Important code snippets or configurations]
- [External resources consulted]
```

---

### Example: Research and Report JWT Token Refresh

**User**: "Use scout to figure out our project's auth logic and then add a JWT token refresh feature."

**Process**:

1.  **Deconstruction & Planning**:

    - **Goal**: Implement JWT refresh.
    - **Areas**: Frontend state management, Backend API.
    - **Scouts**: `Scout A (Frontend)`, `Scout B (Backend)`.
    - **Questions**: Formulate specific questions about token storage, API calls, middleware, and refresh logic.

2.  **First Round of Parallel Scouting**:

    - Launch `Scout A` and `Scout B` simultaneously.
    - `Scout A` finds that the frontend uses an `axios` interceptor and `Redux` to store the token.
    - `Scout B` finds that the backend has `/login` and `/verify-token` endpoints but no `/refresh-token` endpoint.

3.  **Synthesize & Evaluate**:

    - **Findings**: A basic auth flow exists, but the refresh mechanism is missing.
    - **Knowledge Gap**: The backend needs a new `/refresh-token` endpoint. How should it be implemented securely? What should it accept as a credential (e.g., a dedicated refresh token)?

4.  **Iterate or Execute → Iterate**:

    - The information is insufficient to proceed directly. A second round of scouting is needed.

5.  **Second Round of Parallel Scouting (More Focused)**:

    - **New Goal**: Understand secure token refresh patterns and identify implementation location.
    - `Scout A (Documentation & Patterns)`: Responsibility changes to "Search project documentation, existing auth-related code comments, and similar authentication patterns in the codebase for refresh token handling and security notes."
    - `Scout B (Backend Deep Dive)`: Responsibility changes to "Find the most suitable location and implementation method to add a `/refresh-token` endpoint by examining existing auth controller structure, middleware patterns, and route organization."

6.  **Synthesize & Evaluate**:

    - `Scout A` discovers documentation comments in `auth.service.ts` mentioning refresh token security considerations and finds existing `httpOnly` cookie patterns used for session management.
    - `Scout B` identifies that a new method can be added in the `auth.controller.ts` file, following the existing pattern of `login()` and `verifyToken()` methods.
    - **Conclusion**: We now have a clear implementation blueprint based on existing project patterns.

7.  **Iterate or Summarize → Summarize**:

    - Information is now sufficient. Begin final summarize and report.

8.  **Summarize & Report**:

    - Explain to the user: "Through two rounds of scouting, we first understood the existing auth structure, then researched a secure refresh strategy, and finally completed the report..."
