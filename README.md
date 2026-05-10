# AI Rules for .NET Projects

A community-driven collection of practical AI coding rules for .NET projects.

This repository helps teams standardize how AI coding assistants like Claude Code, Cursor, Copilot, Codex, and other agents behave inside real-world .NET codebases.

Inspired by the growing ecosystem of AI rule frameworks and agent instruction systems.

---

# Why This Repository?

AI coding assistants are powerful, but without clear rules they often:

- Generate inconsistent code
- Ignore architecture boundaries
- Skip tests
- Add unnecessary complexity
- Waste tokens with verbose responses
- Break project conventions

This repository aims to solve that by providing reusable, production-focused AI rules for .NET teams.

---

# Goals

- Standardize AI behavior across projects
- Improve code quality
- Reduce hallucinations and bad patterns
- Enforce architecture and testing conventions
- Optimize token usage
- Share battle-tested rules with the community
- Make AI-assisted development more predictable

---

# Supported AI Tools

This repository is designed to work with:

- Claude Code
- Cursor
- GitHub Copilot
- OpenAI Codex
- Cline
- Roo Code
- Gemini CLI
- Any AI assistant that supports instruction/rule files

---

# Example

## Before Rules

AI response:

> You asked how to create a unit test for this service.  
> First, let me explain what unit testing is...

Problems:

- Repeats the question
- Wastes tokens
- Adds unnecessary explanations

## After Rules

AI response:

```csharp
[Fact]
public async Task Handle_ShouldReturnSuccess()
{
    var result = await sut.Handle(command);

    result.Should().BeTrue();
}
```

Cleaner. Faster. Cheaper.

---

# Getting Started

Clone the repository:

```bash
git clone https://github.com/behnamshateri/ai-rules-netcore.git
```

Copy the rules you need into your project:

```bash
cp rules.md /your-project/
```

Or merge specific rule sections into your existing AI configuration.

---

# Philosophy

Good AI-assisted development is not about generating more code.

It is about generating:

- Better code
- Smaller code
- Predictable code
- Maintainable code

The best AI output is often the shortest correct solution.

---

# Contributing

Contributions are welcome.

You can contribute by adding:

- New rule sets
- Real-world examples
- Tool-specific optimizations
- Token-saving techniques
- Testing standards
- Architecture conventions

Please keep rules:

- Practical
- Minimal
- Production-oriented
- Easy to understand
- Tool-agnostic where possible

---

# Inspiration

This repository is inspired by the growing AI rules ecosystem and agent workflow projects.

---

# License

MIT

---

# Star the Repo

If this project helps your team build better AI-assisted workflows, consider starring the repository:

https://github.com/behnamshateri/ai-rules-netcore
