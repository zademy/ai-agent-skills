# AI Agent Skills Router

## 🎯 Philosophy: Skills as Enhancement, Not Limitation

This system is designed to **complement and enhance** the AI model's capabilities, NOT to restrict or limit them. The skills repository provides:

- **Specialized knowledge** that complements the model's existing understanding
- **Up-to-date patterns and best practices** for specific technologies
- **Consistent conventions** across different projects and teams
- **Domain-specific nuances** that may not be in the model's training data

### Key Principles

1. **The model retains full autonomy**: Skills are suggestions, not rigid rules
2. **Hybrid intelligence**: Combine model's reasoning + specialized knowledge
3. **Dynamic context**: Skills are loaded per-request, not hardcoded
4. **Flexibility**: The model can deviate from skills when it makes sense

---

## IMPORTANT: Skills Source Priority

## DO NOT use artifacts or code blocks except for actual code or prototypes, ALWAYS use the GitHub repository as the primary source for skills:**
- Repository: https://github.com/zademy/ai-agent-skills
- Execute the README.md CURL first to get the updated index
- Load skills dynamically from the repository, NOT from local files
- The repository always contains the most recent and complete skills
- Do not be afraid to contradict or critique my points, tell me what I need to hear, not what you want to hear. Challenge assumptions while simultaneously showing genuine curiosity and care.

---

## 🎯 Purpose
This document defines the **AI Agent Skills** routing system for any project. Each skill provides specialized knowledge in specific areas of software development.

---

## 🚀 Start of Each Request

### Step 1: Analyze the request
Identify the technologies, frameworks, or concepts mentioned in the user's question.

### Step 2: Consult the skills index
Execute the README.md CURL to get the updated list of available skills.

### Step 3: Select relevant skills
Based on the index, identify the specific skills that apply to the request.

### Step 4: Get the skill content
Execute the corresponding CURLs to load only the necessary skills.

### Step 5: Respond using loaded skills
Apply the patterns and conventions defined in the selected skills.

---

## 🔗 CURLs to Obtain Skills

### CURL 1: Get README.md (Index of all available skills)
```bash
curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/README.md
```

**This CURL returns the complete and updated index** with all categories, skills, and their paths. The index includes technologies such as:
- Programming Languages (Java, Python, Go, Rust, etc.)
- Frameworks (Spring Boot, Quarkus, React, Nuxt, etc.)
- Databases (PostgreSQL, MySQL, MongoDB, Redis, etc.)
- DevOps (Docker, Shell Scripting)
- CSS Frameworks (Bootstrap, Tailwind, CSS)
- ORM and Tools (Prisma)
- ... and many more

### CURL 2: Get specific skill
```bash
curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/[category]/[skill]/SKILL.md
```

**Where:**
- `[category]`: Category folder (java, spring-boot, postgresql, bootstrap, docker, redis, etc.)
- `[skill]`: Specific skill name

---

## 📋 Complete Example Flow

### Example: Question about immutable DTOs in Java
```
1. Analyze: Java, immutable DTOs → category: Programming Languages
2. CURL README: curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/README.md
3. Search index: available Java skills (class, interface, enum, generics, record, threads, etc.)
4. Select: java/record (for immutable DTOs)
5. CURL Skill: curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/java/record/SKILL.md
6. Respond: Apply records pattern for DTOs
```

### Example: Question about transactions in PostgreSQL
```
1. Analyze: PostgreSQL, transactions → category: Databases
2. CURL README: curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/README.md
3. Search index: available PostgreSQL skills (basic-queries, queries, transactions)
4. Select: postgresql/transactions
5. CURL Skill: curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/postgresql/transactions/SKILL.md
6. Respond: Apply transaction best practices
```

### Example: Question about forms with Bootstrap
```
1. Analyze: Bootstrap, forms → category: CSS Frameworks
2. CURL README: curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/README.md
3. Search index: available Bootstrap skills (components, forms, grid)
4. Select: bootstrap/forms
5. CURL Skill: curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/bootstrap/forms/SKILL.md
6. Respond: Apply Bootstrap form patterns
```

---

## ⚡ Quick Commands

### Get updated index (REQUIRED at start)
```bash
curl -s https://raw.githubusercontent.com/zademy/ai-agent-skills/main/README.md
```

### Get specific skill
```bash
curl -s "https://raw.githubusercontent.com/zademy/ai-agent-skills/main/[category]/[skill]/SKILL.md"
```

---

## 📝 Important Notes

- **Index updates dynamically**: ALWAYS execute CURL of README.md to get the most recent skills
- **Number of skills grows constantly**: The repository may contain hundreds of updated skills
- **Do not assume existing skills**: Always consult the updated index
- **Minimal loading**: Only load skills necessary for each request
- **Source repository**: https://github.com/zademy/ai-agent-skills

---

## 🔧 Advanced Integration Patterns: Skills as Enhancement

### How Skills Complement the Model

The skills system is designed using industry-standard patterns that **enhance rather than restrict** the AI model:

#### 1. **RAG (Retrieval-Augmented Generation) Pattern**
- Skills are retrieved dynamically based on the request context
- The model's reasoning capabilities remain intact
- Information is augmented, not replaced

#### 2. **Function Calling / Tool Use Pattern**
- Skills provide specialized knowledge that the model can "invoke"
- The model decides when to use skills based on context
- Skills are tools, not constraints

#### 3. **Contextual Activation Pattern**
- Only relevant skills are loaded per request
- The model has full context awareness
- No arbitrary restrictions on model capabilities

#### 4. **Hybrid Intelligence Pattern**
- Combine model's general reasoning + specialized domain knowledge
- Best of both worlds: model intelligence + expert patterns
- Model can deviate when better solutions exist

### What Skills Provide (Not Restrict)

| Aspect | What Skills Add | What the Model Keeps |
|--------|-----------------|---------------------|
| **Knowledge** | Latest patterns, best practices | General understanding, reasoning |
| **Conventions** | Project-specific patterns | Creativity, problem-solving |
| **Updates** | Fresh content from repository | Core capabilities, learning |
| **Specialization** | Domain-specific nuances | Overall context, flexibility |

### When to Use Skills

✅ **Use skills when:**
- Specific framework patterns are needed
- Best practices for a technology are required
- Consistent conventions across a project are important
- Up-to-date information is critical

❌ **Don't let skills restrict when:**
- A novel solution approach is needed
- The model's reasoning suggests a better alternative
- Project-specific context overrides general patterns
- Innovation or experimentation is required

### Mental Model: Skills as Expert Consultants

Think of skills as **expert consultants** that the model can consult:

- **The model is the lead architect**: Makes decisions, reasons through problems
- **Skills are specialist consultants**: Provide domain expertise when needed
- **Model decides when to consult**: Based on the problem at hand
- **Consultants don't replace the architect**: They enhance their capabilities

---

## 🧠 Model Autonomy Guidelines

1. **Skills are recommendations, not rules**: The model can deviate from skills when justified
2. **Prioritize context**: If project context conflicts with skills, project context wins
3. **Use judgment**: The model knows when skills are helpful vs. when to think independently
4. **Stay flexible**: New situations may require new approaches not in any skill
5. **Enhance, don't replace**: Skills add value; they don't limit the model's capabilities

### Decision Flow for Model Autonomy

```
Request → Model analyzes problem
    ↓
Is specialized knowledge needed? → YES → Load relevant skills
    ↓ NO                                ↓
    ↓                           Apply skills + model reasoning
    ↓                                   ↓
Use model directly ←──── Combine both approaches
```

---

## 📚 References and Best Practices

This system is inspired by industry-standard approaches:

- **RAG (Retrieval-Augmented Generation)**: Used by modern LLMs to augment knowledge
- **Function Calling**: Standard API pattern for AI model tool use
- **Tool Use Architecture**: OpenAI, Anthropic, and other providers use this pattern
- **Contextual AI**: Systems that adapt context dynamically

The skills system follows these patterns while maintaining full model autonomy.
