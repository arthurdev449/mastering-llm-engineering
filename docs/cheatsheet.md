# LLM Engineering Fast-Track Cheatsheet

A quick-reference guide for the most effective Prompt Engineering (PE) and System Instruction Engineering (SIE) patterns.

---

## 🧠 Reasoning Patterns

### 1. Chain-of-Thought (CoT)
*   **Concept:** Model explicitly lists intermediate steps before the final answer.
*   **Trigger:** "Let's think step by step."
*   **Best For:** Math, logic, and multi-stage planning.

### 2. Tree-of-Thoughts (ToT)
*   **Concept:** Model explores multiple reasoning "branches" and self-evaluates them.
*   **Prompt Pattern:** "List 3 possible approaches to [Task]. Evaluate the pros/cons of each. Select the best one and expand."
*   **Best For:** Creative problem solving and complex design.

### 3. Reflexion / Self-Correction
*   **Concept:** Model critiques its own output in a loop to find errors.
*   **Prompt Pattern:** "Review your previous answer for logic flaws or hallucinations. Provide an improved version."
*   **Best For:** High-accuracy code generation or factual writing.

---

## 🔍 Grounding & Tools

### 4. RAG (Retrieval-Augmented Generation)
*   **Concept:** Injecting relevant external data into the prompt before generation.
*   **Architecture:** `User Query -> Search Engine -> Retrieved Docs -> LLM Prompt -> Answer`.
*   **Best For:** Reducing hallucinations and accessing private/new knowledge.

### 5. ReAct (Reasoning + Acting)
*   **Concept:** Model alternates between reasoning steps and executing tool calls (e.g., Google Search, Calculator).
*   **Cycle:** `Thought -> Action -> Observation -> Thought...`
*   **Best For:** Agentic workflows and live data retrieval.

---

## 🏗 System Architecture (SIE)

### 6. Few-Shot Prompting
*   **Concept:** Providing examples of Input/Output pairs in the system instruction.
*   **Template:**
    ```
    User: 2+2
    Assistant: 4
    User: 10+5
    Assistant: 15
    User: [Target Input]
    ```

### 7. XML-Scoped Instructions
*   **Concept:** Using `<Tag>` structures to clearly demarcate rules, roles, and constraints.
*   **Benefit:** Prevents "Instruction Drift" in long context sessions.
*   **Example:**
    ```xml
    <Constraints>
      - No social talk.
      - Output JSON only.
    </Constraints>
    ```

---

## ⚡ Parameter Reference

| Parameter | Function | Typical Use Case |
| :--- | :--- | :--- |
| **Temperature** | Controls randomness (0.0 - 2.0) | 0.0 for code/facts; 0.8+ for creative. |
| **Top P** | Nucleus sampling (cuts off tail) | Alternative to Temperature; usually set to 1. |
| **Stop Sequences** | Tokens that halt generation | `\n`, `User:`, `</s>`. |
| **Frequency Penalty** | Reduces repetition of words | Helpful for long-form narrative. |
