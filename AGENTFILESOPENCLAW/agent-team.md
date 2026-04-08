# 🤖 Agent Team Handbook — OpenClaw RAG System

> Reference guide for all agents and the owner.
> Read this before starting any task.

---

## QUICK REFERENCE — WHO DOES WHAT

| I need to... | Talk to... |
|---|---|
| Assign a new feature | Manager Agent |
| Design a new system component | Architect Agent |
| Write or fix code | Builder Agent |
| Improve search quality | AI/RAG Agent |
| Upload or clean a new manual | Data Agent |
| Automate a process | Workflow & Tools Agent |
| Redesign the UI | UI/UX Agent (on-demand) |

---

## HOW TO GIVE INSTRUCTIONS TO YOUR AGENT TEAM

### ✅ GOOD instruction (specific, actionable)
```
Manager Agent: The technician needs to search by equipment serial number.
Have the Architect Agent design the data model, then Builder Agent implement
the search filter on the results page. Flag any DB schema changes for my approval.
```

### ❌ BAD instruction (vague)
```
Make search better
```

---

## OWNER INTERVIEW PROTOCOL

Before starting any major feature, the Architect Agent MUST interview the owner.
Use these question categories:

**1. Problem Definition**
- What specific problem does this feature solve?
- Who experiences this problem? (mechanic, supervisor, admin?)
- How do they currently solve it without this feature?

**2. Success Criteria**
- How will we know this feature is working correctly?
- What does \"done\" look like?
- Are there performance targets? (e.g., search results in <2 seconds)

**3. Constraints**
- Any technology constraints?
- Does it need to work offline?
- Mobile or desktop priority?

**4. Owner Experience / Domain Knowledge**
- Have you seen this done well elsewhere?
- Any specific workflows from your experience we should mirror?
- What are the most common mistakes technicians make that this should prevent?

---

## TASK LIFECYCLE

```
1. Owner gives instruction to Manager Agent
 ↓
2. Manager Agent breaks into subtasks, assigns agents
 ↓
3. Architect Agent designs approach (if needed)
 ↓
4. Decision required? → Write to /docs/decisions.md → Wait for owner approval
 ↓
5. Builder/Data/RAG Agent executes on feature branch
 ↓
6. Tests written and passing
 ↓
7. Manager Agent reviews, summarizes work done
 ↓
8. Owner reviews PR → Merges to main
```

---

## BRANCH NAMING CONVENTION

```
feature/[agent]-[short-description]
fix/[agent]-[short-description]
data/[ingestion-task-name]

Examples:
feature/builder-serial-number-search
fix/rag-reranking-accuracy
data/caterpillar-d6-manual-ingestion
```

---

## DAILY STANDUP FORMAT (Manager Agent reports)

```
## Standup — [DATE]

### ✅ Completed Yesterday
- [Agent]: [What was done]

### 🔨 In Progress Today
- [Agent]: [What is being worked on]

### 🚧 Blocked
- [Agent]: [What is blocking them and what they need]

### 📋 Awaiting Owner Approval
- [Link to decision in /docs/decisions.md]
```

---

## OWNER EXPERIENCE TO EMBED IN SYSTEM

> Fill this section in as we interview you. This becomes the domain knowledge
> layer that makes the RAG system smarter than a generic document search.

- Common mistakes technicians make: _[to be filled]_
- Most-searched document types: _[to be filled]_
- Critical warnings that must always surface: _[to be filled]_
- Equipment types in scope: _[to be filled]_
- Terminology specific to your operation: _[to be filled]_
