# AI prompt templates

Rules I follow (from my study plan):
- **AI-off for first attempts**: Odin projects, Exercism/Codewars, DSA, Anki cards, and the first version of each flagship feature.
- **20-minute rule**: stuck for 20 minutes → ask for a *hint*, not code.
- **Explain-back**: before committing AI-touched code, I explain every line out loud or in a note.
- **Version check**: `jakarta.*` not `javax.*`; Spring Boot 4 / Spring 7; Next.js App Router; no Create React App.
- **Mutation-check** any AI-written test (break the code on purpose — the test must fail).
- No secrets or personal data in prompts.

---

## 1. Challenge (make me a practice task)
```
I'm learning [topic] in [language/version]. Give me one practice exercise at
[beginner/intermediate] level that uses [specific concepts]. Give only the task
description and 3 example inputs/outputs. Do not give a solution or hints.
```

## 2. Hint (after 20 minutes stuck)
```
I'm working on [exercise]. Here is my attempt:
[code]
Here is what happens: [error / wrong output].
Here is what I've tried: [list].
Give me ONE hint pointing to where my thinking is wrong. Do not write code
and do not give the fix.
```

## 3. Review (after my solution works)
```
Review my [language] solution as a senior developer would in a code review.
[code]
List issues by priority: correctness, readability, idiomatic [language version]
style, performance. For each, explain WHY and point to the line, but let me
write the fix myself.
```

## 4. Test generation (Phase 3 onward)
```
Here is a [class/function] and its intended behaviour:
[code + spec]
Suggest test cases (names + inputs + expected results) that cover normal cases,
edge cases and error cases, using [JUnit 5 / Jest / pytest]. List cases first;
I'll ask for code separately.
```
After: mutation-check every generated test.

## 5. Debugging
```
Stack trace / error:
[paste]
Relevant code:
[paste]
Environment: [Java 25 / Spring Boot 4 / OS]
What I expected vs what happened: [...]
Explain what the error message means and list the 2–3 most likely causes in
order. Don't give me the fix yet.
```
