# General Rules

## General Direction
- **Paradigm:** Prefer **Pure Functions** and **Dependency Injection**. Isolate side effects.
- **Error Handling:** Fail loud. Prefer `throw` without `catch`. Only catch if transforming the error or strictly recovering. **Never silence errors.**
- **Agentic Hygiene:** If acting as an AI agent, verify your own logic line-by-line. Aggressively prune redundant comments and tests that "mock the mock."

## Code Style
- **Indentation:** Flatten code using **early returns** (`continue`, `return`, `break`) to avoid deep `if/else` nesting.
- **Naming:** Prefix functions with `maybe_` if they can return `None`/`null`/`undefined` (e.g., `maybe_get_user`).
- **Docstrings:** Context is king. Explain *why* or *how* (non-trivial info). **Forbidden:** One-liner docstrings that just repeat the function name.
- **Imports:** Always place imports at the **top-level** of the module. Never import inside functions.
- **Boolean Logic:** Use implicit checks (`if obj:`) generally. Explicitly check for `0` or empty strings only if they are valid values. Avoid double negation.

## Plan Style
- **Context First:** Before writing code, verify you have the service layer context. Do not guess database schemas.
- **Scope Definition:** clearly define what is in scope vs. out of scope.
- **Review Prep:** When generating PR descriptions or summaries, include the "Why", the "Scope", and explicitly mention any "Agentic" limitations (e.g., "Tests need human verification").

## Test Style
- **Structure:** Use **standalone functions** (no classes). Keep tests short, focused, and flat.
- **Mocking:** **Avoid mocking** whenever possible. Prefer testing against real helpers, pure logic, or lightweight fakes.
  - If mocking is unavoidable (e.g., 3rd party APIs), use specific tools like `mocker.patch.object` (Python) or `vi.spyOn` (JS), but never mock internal implementation details unnecessarily.
- **Parameterization:** Heavily prefer table-driven tests (`pytest.mark.parametrize` in Python, `test.each` in JS/TS) to deduplicate logic and cover edge cases efficiently.
- **Reusability:** Share fixtures for data setup. Do not duplicate setup logic across multiple tests.
- **Philosophy:** Optimize for high testability by designing pure functions first. Test the output, not the internal state.

---

# Python

- **Typing Syntax:** Exclusively use **PEP 604** Union types (`X | Y`) instead of `Union[X, Y]` or `Optional[X]`.
- **Testing Implementation:**
  - Use `pytest` style fixtures and parameterization.
  - Create reusable fixtures for data/mocks; do not repeat setup.

---

# Typescript/Javascript

- **Typing:** **Strict TypeScript**. Avoid `any` unless absolutely unavoidable.
- **State Management:**
  - Keep `useEffect` simple. Read "You might not need an effect" guidelines.
  - Invalidate React Query caches after mutations.
- **Validation:**
  - **Frontend:** Surface Zod errors to the user (UX only).
  - **Backend:** Rely on Pydantic for actual security/integrity.
- **UI/UX:**
  - Use `visibility` or `opacity` for hiding components with animations (avoid breaking layout).
  - Test scrolling behavior on long content.
  - Ensure Dark Mode compatibility (no hardcoded hex black/white on text).
