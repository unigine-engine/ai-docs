# UNIGINE 2.21 Project

## Engine Documentation

`ai_docs/` contains the full UNIGINE 2.21 documentation. Search here before writing any engine code.

- `ai_docs/README.md` — engine key concepts, conventions, and common pitfalls. **Read this first** — it covers coordinate system, component lifecycle, physics rules, and other things that differ from other 3D engines
- `ai_docs/md_docs/SUMMARY.md` — flat index of all documentation pages with brief descriptions. Use this for searching by keyword
- `ai_docs/md_docs/` — full engine documentation: API reference (one file per class), guides, and concepts (~2000 pages). Each API page contains method signatures, parameters, return types, and code examples
- `ai_docs/cpp_samples/` — C++ code examples. Each sample is a folder with README.md (description), source files (.cpp/.h), and .world scene file
- `ai_docs/cs_samples/` — C# code examples (same structure, .cs files)

## CRITICAL RULES

These rules are non-negotiable. Violating them produces broken code and wastes the user's time.

1. **ALWAYS search docs before using ANY UNIGINE API.**
   UNIGINE API names are unique to this engine. They do NOT match Unity, Unreal, Godot, or any other engine. Search by TASK, not by guessed method name.
   - ✗ WRONG: assume `Input::isKeyPressed()` exists because it sounds right
   - ✓ RIGHT: search `ai_docs/md_docs/` for "keyboard input" → find `Input::isKeyDown()`

2. **NEVER fabricate method names, parameter types, console commands, or Editor menu items.**
   If you cannot find it in documentation — say so. Do not invent plausible-sounding names. This includes:
   - API methods (e.g. `AddNormal()`, `Node.IsValid()` — do not exist in C#)
   - Console commands (e.g. `component_system_reload` — does not exist)
   - Editor UI (e.g. "Tools → Reload Component System" — does not exist)
   - Enum values — verify exact names (e.g. `Input.KEY.DIGIT_1`, not `KEY.ONE`)

3. **"I don't know" is a valid answer.**
   An honest "not found in documentation" is always better than a confident wrong answer. If you answer from general knowledge, you MUST explicitly warn the user.

4. **Read `ai_docs/README.md` before your first UNIGINE task in this session.**
   It contains engine-specific conventions that override general gamedev knowledge.

5. **Search samples BEFORE writing code. Copy and adapt.**
   ALWAYS search `ai_docs/cs_samples/` or `ai_docs/cpp_samples/` for a working example of your task BEFORE writing any code. **Copy and adapt sample code** rather than writing from scratch — even if the sample is not a perfect match. Search by task keyword (e.g. "shooting", "intersection", "gui"), not by API name.

6. **List → verify → THEN write code.**
   Before writing any .cs or .cpp file:
   1. List every UNIGINE API method, property, and enum you plan to use
   2. Grep `ai_docs/md_docs/api/library/` for each one — confirm it exists and check the exact signature
   3. Only start writing code after ALL methods are confirmed
   Do NOT write code first and verify after — this wastes time on compilation errors.

## IMPORTANT RULES

7. **UNIGINE ≠ other engines.** Do not transfer assumptions from Unity/Unreal/Godot. Same-sounding concepts may work differently.

8. **C++ API ≠ C# API.** Method names, patterns, and available members differ between C++ and C#. Do not assume a C++ method exists in C#:
   - C++: `node->setWorldPosition(pos)` → C#: `node.WorldPosition = pos` (property, not method)
   - C++: `node.isValid()` (Ptr<> method) → C#: no equivalent (`node != null` for managed refs)
   - C++: `getIFps()` → C#: `Game.IFps` (property)
   Always verify in the **correct language** docs.

9. **Incomplete answer > invented answer.** When listing elements of a system, warn that the list may be incomplete rather than padding with guesses.

10. **Do not make decisions for the user.** Build configuration, launch method, architecture choices — present options and let the user choose.

11. **Explore the project before coding.** At the start of a session, read project files to understand what already exists. Template projects contain existing assets — know what you're working with.

12. **Ask the user when stuck.** If you spend more than 3 tool calls trying to fix a single issue without progress — stop and ask the user for help. Do NOT attempt destructive workarounds (like `world_reload`, deleting files, or fabricating commands) on your own.

13. **Components require a build step.** After writing component code (.cs/.cpp):
    1. Propose building the project to check for compilation errors (wait for user approval)
    2. After a successful build, tell the user how to make the component available:
       - C#: make the Editor window active (it auto-detects and recompiles)
       - C++: build (if not already built) and run the application (components are initialized at startup together with the component system)
    Components do not appear in the Editor until these steps are completed.

## VERIFICATION CHECKLIST

Before finalizing any UNIGINE API usage, verify:
- [ ] Method name found in `ai_docs/md_docs/` (not assumed)
- [ ] Verified in the correct language (C# vs C++, not mixed)
- [ ] Parameter types match documentation (e.g. `mat3` vs `mat4`, `vec3` vs `dvec3`)
- [ ] Enum values are exact (grep for the enum, don't guess names)
- [ ] Return type handled correctly
- [ ] Console commands verified in docs (do NOT fabricate)
- [ ] If any step fails — search again or tell the user honestly

## SEARCH STRATEGY

1. Start with samples — grep `ai_docs/cs_samples/SUMMARY.md` or `ai_docs/cpp_samples/SUMMARY.md` for your task keyword to find a relevant example
2. Grep `ai_docs/md_docs/SUMMARY.md` for your keyword — do NOT read the entire file
3. If no results — search directly in `ai_docs/md_docs/` by keyword
4. For API signatures — grep in `ai_docs/md_docs/api/library/` (do NOT read entire API files — grep for the specific method)
5. If still not found — tell the user. Warn explicitly before answering from general knowledge

**Search efficiently:** grep for specific methods/keywords, do NOT read entire large API reference files. Target your search.