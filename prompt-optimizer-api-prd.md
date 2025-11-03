# 🚀 Prompt Optimizer API - Product Requirements Document

> **Vibe Coding Edition** 🎯  
> _"Compress smart, preserve meaning, ship fast"_

---

## 📋 Document Info

| Field | Value |
|-------|-------|
| **Product Name** | Prompt Optimizer API |
| **Version** | 1.0 (MVP) |
| **Status** | Ready to Build 🔨 |
| **Target** | API-Only (No Frontend) |
| **Inspiration** | [DeepMyst Platform](https://platform.deepmyst.com) |

---

## 🎯 Mission Statement

Build a **token optimization API** that intelligently compresses prompts (up to 300K tokens) while **preserving meaning, context, and intent**. Think of it as a smart minifier for LLM prompts—removing the fluff without losing the soul.

---

## 🔥 The Problem

**LLMs are expensive AF.** Every token costs money, and most prompts are bloated with:
- Redundant words and phrases
- Excessive politeness and filler
- Repeated context and boilerplate
- Unnecessary whitespace and formatting
- Verbose instructions that could be terse

**We need:** An API that takes a verbose prompt and returns a lean, mean, optimized version that's cheaper to run but just as effective.

---

## 🎨 Core Concept (Inspired by DeepMyst)

DeepMyst is an intelligent LLM gateway that:
- Reduces token usage through sophisticated compression
- Preserves content quality and meaning
- Works as middleware between apps and LLM providers
- Achieves 20-60% compression ratios in real-world scenarios

**Our API will replicate their token optimization logic** with a focus on:
- **Rule-based optimization** (MVP)
- **Semantic preservation** (no meaning loss)
- **Production-ready robustness** (handle 300K tokens)

---

## 🏗️ Architecture Overview

```
┌─────────────────────┐
│   Client Request    │
│  (Large Prompt)     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   API Gateway       │
│  /api/v1/optimize   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Optimizer Engine   │
│                     │
│  ┌───────────────┐  │
│  │ Basic Mode    │  │
│  │ (Rule-based)  │  │
│  └───────────────┘  │
│                     │
│  ┌───────────────┐  │
│  │ Advanced Mode │  │
│  │ (Future LLM)  │  │
│  └───────────────┘  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Optimized Output  │
│   + Statistics      │
└─────────────────────┘
```

---

## 🎬 API Specification

### **Endpoint:** `POST /api/v1/optimize`

### **Request Body:**
```typescript
{
  "prompt": string,          // The prompt to optimize (up to 300K tokens)
  "mode": "basic" | "advanced"  // Optimization mode
}
```

### **Response Body:**
```typescript
{
  "optimized_output": string,  // The compressed prompt
  "stats": {
    "original_chars": number,     // Character count before
    "optimized_chars": number,    // Character count after
    "compression_percentage": number,  // % reduction (e.g., 32.5)
    "original_tokens": number,    // Estimated tokens before
    "optimized_tokens": number,   // Estimated tokens after
    "token_savings": number       // Tokens saved
  },
  "mode_used": "basic" | "advanced",
  "processing_time_ms": number
}
```

### **Example Request:**
```json
{
  "prompt": "Can you please provide me with a detailed summary of the following text? I would really appreciate it if you could help me understand the main points. The text is: The quick brown fox jumps over the lazy dog. This is a common English pangram.",
  "mode": "basic"
}
```

### **Example Response:**
```json
{
  "optimized_output": "Summarize: The quick brown fox jumps over the lazy dog. Common English pangram.",
  "stats": {
    "original_chars": 234,
    "optimized_chars": 87,
    "compression_percentage": 62.8,
    "original_tokens": 52,
    "optimized_tokens": 19,
    "token_savings": 33
  },
  "mode_used": "basic",
  "processing_time_ms": 45
}
```

---

## 🛠️ Feature Breakdown

### **1. Basic Mode (MVP - Implement This)**

Rule-based optimization using smart heuristics and NLP. **NO LLM CALLS.**

#### **Optimization Techniques:**

##### **A. Context Compression**
- ✂️ Remove redundant phrases and boilerplate
- 🔄 Deduplicate repeated information
- 📦 Collapse multi-line whitespace
- 🎯 Preserve unique facts and key entities

**Example:**
```
Input: "I would like to ask you to please help me with this task. Can you please..."
Output: "Help with this task. Can you..."
```

##### **B. Instruction Simplification**
- 🗑️ Strip excessive politeness ("please", "could you", "I would appreciate")
- ⚡ Convert verbose commands to terse imperatives
- 🎯 Keep only essential directive words

**Example:**
```
Input: "Can you please provide me with a list of the main features?"
Output: "List main features."
```

##### **C. Entity Canonicalization**
- 🏷️ Use shortnames for repeated entities
- 📝 Create glossary for long technical terms
- 🔗 Maintain entity consistency throughout

**Example:**
```
Input: "The United States of America has... The United States of America requires..."
Output: "USA has... USA requires..."
```

##### **D. Dynamic Truncation**
- ✂️ Limit prompt length intelligently
- 🎯 Prioritize recent and unique information
- 📚 Summarize or truncate repeated historical context

**Example:**
```
Input: User chat with 50 messages of "hello" and "how are you"
Output: Latest 5 unique interactions only
```

##### **E. Output Guidance Injection**
- 📋 Add format hints: "respond as list", "be concise", "bullet points"
- 🎯 Guide model to produce tighter outputs
- ⚡ Reduce unnecessary elaboration from model

##### **F. Whitespace & Formatting Optimization**
- 🗜️ Compress multiple spaces to single space
- 🔪 Remove trailing/leading whitespace
- 📄 Convert multi-line breaks to single breaks
- 🧹 Strip unnecessary markdown/formatting

---

### **2. Advanced Mode (Future Enhancement - DON'T Implement Yet)**

**Status:** 🚧 Placeholder for LLM-based optimization

**Behavior in MVP:**
- Runs **Basic Mode first** (all rule-based optimizations)
- Skips LLM-based compression (not implemented)
- Returns same output as Basic Mode
- Response indicates `"mode_used": "advanced"` but same result

**Future Implementation:**
- Will use an LLM (e.g., GPT-4, Claude) to semantically compress
- Rephrase verbose instructions to minimal equivalents
- Use context understanding to drop low-value tokens
- Employ techniques like LLMLingua or prompt distillation

---

## 📐 Technical Requirements

### **Optimization Constraints & Guardrails**

#### **1. Preserve Meaning & Intent**
- ✅ **MUST NOT** change semantic meaning
- ✅ **MUST** keep all critical instructions
- ✅ **MUST** maintain entity distinctions
- ✅ **MUST** preserve numerical values exactly

#### **2. Hierarchy Preservation**
```
System Instructions > Developer Instructions > User Instructions
```
- 🚫 Never drop safety/compliance instructions
- 🚫 Never reveal hidden system prompts
- 🚫 Never invent facts not in original

#### **3. Content Guardrails**
- 📌 Preserve citations and quotes verbatim
- 🔢 Keep all numbers and measurements exact
- 🏷️ Maintain technical terms and proper nouns
- 📋 Retain input/output format specifications

#### **4. Budgeting & Prioritization**
- 🎯 Prioritize "must-keep" instructions
- ⚖️ Graceful degradation if over token budget
- 📊 Favor recent context over historical
- 🔥 Drop low-ROI tokens first

#### **5. Quality Metrics**
- Target: **20-60% compression ratio**
- Preserve: **95%+ named entities**
- Maintain: **98%+ instruction fidelity**
- Speed: **< 2 seconds** for 300K token input

---

## 🧩 Implementation Guidelines

### **Technology Stack (Suggested)**

| Component | Recommendation |
|-----------|----------------|
| **Language** | TypeScript/Node.js |
| **Framework** | Express or Fastify |
| **NLP Library** | compromise.js or natural (for entity detection) |
| **Token Counter** | tiktoken (OpenAI tokenizer) or gpt-tokenizer |
| **Validation** | Zod or Joi |
| **Testing** | Jest + supertest |

### **Optimization Pipeline (Pseudo-code)**

```typescript
async function optimizePrompt(prompt: string, mode: string): Promise<OptimizedResult> {
  // Step 1: Parse and analyze
  const entities = extractEntities(prompt);
  const instructions = extractInstructions(prompt);
  const context = extractContext(prompt);
  
  // Step 2: Apply rule-based optimizations
  let optimized = prompt;
  
  // Whitespace compression
  optimized = compressWhitespace(optimized);
  
  // Politeness stripping
  optimized = stripPoliteness(optimized);
  
  // Redundancy removal
  optimized = deduplicateContent(optimized);
  
  // Entity canonicalization
  optimized = canonicalizeEntities(optimized, entities);
  
  // Instruction simplification
  optimized = simplifyInstructions(optimized, instructions);
  
  // Context compression
  optimized = compressContext(optimized, context);
  
  // Output guidance
  optimized = addOutputGuidance(optimized);
  
  // Step 3: Validate meaning preservation
  validateSemanticFidelity(prompt, optimized);
  
  // Step 4: Compute stats
  const stats = computeStats(prompt, optimized);
  
  // Step 5: Return result
  return { optimized_output: optimized, stats };
}
```

---

## 🎯 Success Criteria

| Metric | Target |
|--------|--------|
| **Compression Ratio** | 20-60% token reduction |
| **Semantic Preservation** | 98%+ meaning retention (manual review) |
| **Entity Preservation** | 95%+ named entities intact |
| **Processing Speed** | < 2s for 300K tokens |
| **API Uptime** | 99.9% availability |
| **Error Rate** | < 0.1% failed requests |

---

## 🧪 Testing Strategy

### **Unit Tests**
- Test each optimization function independently
- Verify entity preservation
- Check instruction simplification
- Validate whitespace compression

### **Integration Tests**
- End-to-end API request/response
- Large prompt handling (100K, 200K, 300K tokens)
- Mode switching (basic vs advanced)
- Error handling and edge cases

### **Quality Tests**
- Manual review of 100 sample optimizations
- Semantic similarity scoring (cosine similarity on embeddings)
- A/B testing with LLM outputs (original vs optimized)

### **Performance Tests**
- Load testing: 1000 concurrent requests
- Latency testing: p50, p95, p99
- Memory profiling for large inputs

---

## 📊 Example Test Cases

### **Test Case 1: Politeness Stripping**
```typescript
Input: "Could you please help me understand how to implement this feature? I would really appreciate your assistance."
Expected: "Help me implement this feature."
Compression: ~60%
```

### **Test Case 2: Context Deduplication**
```typescript
Input: "The user said hello. The user asked how are you. The user said hello again. The user asked about the weather."
Expected: "User: hello, how are you, hello again, weather question."
Compression: ~45%
```

### **Test Case 3: Entity Canonicalization**
```typescript
Input: "The United States of America and the United States of America's policies..."
Expected: "USA and USA's policies..."
Compression: ~30%
```

### **Test Case 4: Instruction Simplification**
```typescript
Input: "I need you to analyze the following data and provide me with a comprehensive summary of the key insights."
Expected: "Analyze data. Summarize key insights."
Compression: ~55%
```

### **Test Case 5: Large Context Truncation**
```typescript
Input: 50-message chat history with repeated greetings
Expected: Last 10 unique interactions
Compression: ~70%
```

---

## 🚀 Deliverables

### **Phase 1: MVP (Current Scope)**
- ✅ API endpoint `/api/v1/optimize`
- ✅ Basic mode (rule-based optimization)
- ✅ Advanced mode (placeholder, returns Basic mode result)
- ✅ Comprehensive stats in response
- ✅ Unit tests + integration tests
- ✅ Performance benchmarks
- ✅ API documentation (OpenAPI/Swagger)

### **Phase 2: Future Enhancements (Out of Scope)**
- 🔮 Advanced mode with LLM-based optimization
- 🔮 Streaming optimization for real-time use
- 🔮 Multi-language support
- 🔮 Custom optimization profiles
- 🔮 Caching layer for repeated prompts

---

## 🎨 Optimization Strategies Deep Dive

### **1. Politeness & Filler Removal**

**Target Phrases:**
```typescript
const FILLER_PHRASES = [
  "could you please",
  "I would appreciate",
  "if you don't mind",
  "I was wondering if",
  "it would be great if",
  "can you help me with",
  "I need you to",
  "I want you to",
  "please provide me with",
  "I would like to request"
];
```

**Replacement Strategy:**
- Remove entirely or replace with imperative verb
- Example: "Could you please list" → "List"

---

### **2. Redundancy Detection**

**Techniques:**
- N-gram overlap detection (find repeated phrases)
- Semantic similarity using embeddings (cosine > 0.9)
- Exact substring matching
- Temporal deduplication (keep only latest occurrence)

**Example:**
```typescript
// Before
"The API returns JSON. The API also provides XML. The API response is fast."

// After
"API returns JSON, XML. Response is fast."
```

---

### **3. Entity Shortening**

**Rules:**
- Use acronyms for long organization names
- Use common abbreviations (United States → USA)
- Create glossary for technical terms
- Maintain consistency across prompt

**Glossary Example:**
```typescript
{
  "The United States of America": "USA",
  "Machine Learning Model": "ML Model",
  "Application Programming Interface": "API",
  "Natural Language Processing": "NLP"
}
```

---

### **4. Context Windowing**

For chat histories or long contexts:

**Strategy:**
- Keep last N messages (recency bias)
- Summarize older context in one line
- Preserve unique information only
- Drop repeated greetings/acknowledgments

**Example:**
```typescript
// Before (1000 tokens)
User: Hello
Bot: Hi!
User: How are you?
Bot: I'm good!
[... 50 similar exchanges ...]

// After (100 tokens)
[Earlier: greetings & small talk]
[Recent 5 exchanges with unique info]
```

---

### **5. Output Guidance Injection**

Add meta-instructions to guide model:

**Templates:**
```typescript
const OUTPUT_GUIDES = [
  "Respond concisely.",
  "Use bullet points.",
  "Answer in 3 sentences max.",
  "List format only.",
  "No explanations, just results."
];
```

**Placement:** End of prompt or beginning

---

## 📝 Edge Cases & Error Handling

### **1. Malformed Input**
- **Issue:** Non-string or empty prompt
- **Response:** `400 Bad Request` with clear error message

### **2. Over-sized Input**
- **Issue:** Prompt > 300K tokens
- **Response:** `413 Payload Too Large` with token count

### **3. Optimization Failure**
- **Issue:** Output is longer than input (rare)
- **Response:** Return original prompt with note

### **4. Invalid Mode**
- **Issue:** Mode is not "basic" or "advanced"
- **Response:** `400 Bad Request` with allowed values

### **5. Timeout**
- **Issue:** Processing takes > 30 seconds
- **Response:** `504 Gateway Timeout`

---

## 🔐 Security & Compliance

### **Data Privacy**
- ❌ Do NOT log full prompts (may contain PII)
- ✅ Log only metadata (length, mode, timestamp)
- ✅ Implement request ID for debugging

### **Rate Limiting**
- 🚦 Implement rate limiting per API key
- 🚦 Suggested: 100 requests/minute per user
- 🚦 Return `429 Too Many Requests` when exceeded

### **Input Sanitization**
- 🛡️ Sanitize against injection attacks
- 🛡️ Validate UTF-8 encoding
- 🛡️ Strip control characters

---

## 📚 Documentation Requirements

### **API Documentation (OpenAPI 3.0)**
```yaml
openapi: 3.0.0
info:
  title: Prompt Optimizer API
  version: 1.0.0
  description: Optimize prompts to reduce token costs while preserving meaning

paths:
  /api/v1/optimize:
    post:
      summary: Optimize a prompt
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                prompt:
                  type: string
                  maxLength: 300000
                mode:
                  type: string
                  enum: [basic, advanced]
      responses:
        200:
          description: Successfully optimized
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/OptimizedResponse'
```

### **README.md**
- Quick start guide
- API usage examples
- Optimization techniques explained
- Performance benchmarks
- Troubleshooting

### **Developer Guide**
- Architecture overview
- Code structure
- Adding new optimization rules
- Testing guide

---

## 🎯 Key Principles (The Vibe)

1. **🚫 Never sacrifice meaning for compression**
   - If in doubt, keep the token

2. **⚡ Speed is a feature**
   - Target < 2s for 300K tokens
   - Optimize hot paths

3. **🧹 Clean code, clean prompts**
   - Well-tested, maintainable codebase
   - Clear separation of concerns

4. **📊 Measure everything**
   - Log compression ratios
   - Track processing times
   - Monitor quality metrics

5. **🛡️ Fail gracefully**
   - Return original if optimization fails
   - Clear error messages
   - Never crash

6. **🎯 KISS (Keep It Simple, Stupid)**
   - Rule-based first, LLM later
   - No over-engineering
   - Ship fast, iterate

---

## 🎬 Getting Started (For Developers)

### **Step 1: Set Up Project**
```bash
# Initialize project
npm init -y
npm install express zod tiktoken dotenv

# Install dev dependencies
npm install -D typescript @types/node @types/express jest ts-jest
```

### **Step 2: Core Files to Create**
```
src/
├── index.ts              # API server entry point
├── routes/
│   └── optimize.ts       # /api/v1/optimize route
├── services/
│   └── optimizer.ts      # Core optimization logic
├── utils/
│   ├── tokenCounter.ts   # Token counting utility
│   ├── entityExtractor.ts # Entity detection
│   └── validator.ts      # Input validation
└── tests/
    ├── optimizer.test.ts
    └── api.test.ts
```

### **Step 3: Implement Optimizer Service**
- Start with whitespace compression
- Add politeness stripping
- Implement entity canonicalization
- Build deduplication logic
- Add instruction simplification
- Integrate all optimizations

### **Step 4: Build API Layer**
- Define routes with Express
- Add input validation with Zod
- Implement error handling
- Add request logging

### **Step 5: Test Everything**
- Write unit tests for each optimization
- Add integration tests for API
- Manual QA with diverse prompts
- Performance benchmarking

### **Step 6: Document & Deploy**
- Write API docs (OpenAPI spec)
- Create usage examples
- Deploy to hosting platform

---

## 🔥 Success Metrics Dashboard (Post-MVP)

Track these metrics in production:

| Metric | Target | Current |
|--------|--------|---------|
| Average Compression Ratio | 30-50% | TBD |
| P95 Latency | < 2s | TBD |
| API Uptime | 99.9% | TBD |
| Error Rate | < 0.1% | TBD |
| Requests per Day | 10,000+ | TBD |
| User Satisfaction | > 4.5/5 | TBD |

---

## 🎊 Final Notes

**This is MVP territory.** Build the basics exceptionally well:
- Robust rule-based optimization
- Fast, reliable API
- Clear, helpful error messages
- Comprehensive tests

**Don't over-engineer.** LLM-based optimization is cool but out of scope for now. Nail the fundamentals first.

**Preserve meaning above all.** A 70% compression that loses key context is worthless. A 30% compression that keeps everything intact is gold.

**Ship it. Measure it. Improve it.** Get this into production, gather real-world data, then iterate.

---

## 📎 Appendix

### **Useful Resources**
- [DeepMyst Documentation](https://docs.deepmyst.com/introduction)
- [LLMLingua Paper](https://arxiv.org/abs/2310.05736) (for future reference)
- [Prompt Compression Guide](https://www.datacamp.com/tutorial/prompt-compression)
- [tiktoken Library](https://github.com/openai/tiktoken)
- [compromise.js NLP](https://github.com/spencermountain/compromise)

### **Sample Compression Benchmarks (From Research)**
| Use Case | Original Tokens | Optimized Tokens | Compression |
|----------|----------------|------------------|-------------|
| Customer Support | 200 | 130 | 35% |
| Code Documentation | 450 | 280 | 38% |
| Chat History | 1000 | 350 | 65% |
| RAG Context | 3000 | 1800 | 40% |

---

## ✅ Ready to Build?

**You have everything you need:**
- Clear product vision
- Detailed API spec
- Optimization strategies
- Technical guidelines
- Testing framework
- Success metrics

**Now go build something awesome.** 🚀

---

_Document Version: 1.0_  
_Last Updated: 2025-11-03_  
_Status: Ready for Implementation ✅_

