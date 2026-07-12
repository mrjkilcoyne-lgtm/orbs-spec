# Python

## Scope
Idiomatic modern Python (3.10+): typing, packaging, async, and the standard library.

## Core principles
- Pythonic means using the language's grain: comprehensions, unpacking, context managers, iterators — not translated Java.
- Duck typing plus gradual type hints: annotate public boundaries, run mypy/pyright in CI.
- The GIL serializes CPU-bound threads; use multiprocessing or native extensions for CPU work, asyncio/threads for IO.
- Mutable default arguments are evaluated once — a classic footgun; default to None.
- Explicit is better than implicit: the Zen is an actionable review checklist.

## Apex practices
- One venv per project, lockfile-managed (uv/poetry); never install into system Python.
- Use dataclasses/pydantic for data shapes, `pathlib` over os.path, f-strings, `enumerate`/`zip` over index math.
- Context managers for every resource; `contextlib` for custom ones.
- Profile with cProfile/py-spy before optimizing; often the answer is a C-backed library (numpy) not micro-tuning.

## Pitfalls
- Catching bare `except:` (swallows KeyboardInterrupt/SystemExit).
- Late-binding closures in loops capturing the last value.
- Shadowing stdlib module names (json.py, email.py) causing baffling imports.

## Tools & references
uv, ruff, pyright/mypy, pytest, py-spy; "Fluent Python" (Ramalho).
