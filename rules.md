This file provides guidance to use any AI agaent when working with code in this repository.

## Common Development Commands
- Build: `dotnet build` (targets .NET 8.0 via Directory.Build.props)
- Lint: Supported through analyzers configured in Directory.Build.props (Sonar, StyleCop)
- Test: `dotnet test` (includes unit/acceptance tests per test project structure)
- Run tests directly: Use `dotnet test <test-project>` (e.g., `dotnet test WebApi.Tests`)

## Code Architecture Overview
1. **Core Modules**
   - `WebApi`: Primary API handling dispensation logic, including third-party integrations (Vektis, DAC)
   - `BL`: Business logic services (e.g., `Resturant` module under review for new API migration)
   - `Data`: Persistence layer (contains DbMigrations and DataAccessContext)

## Unit tests rules
- Unit tests should be written for all code paths
- Always use `Arrange-Act-Assert` pattern for unit tests
- Dont use `using var` in unit tests
- Dont use comments in unit tests
- Use fluent assertions for unit tests
- Services.Impmentnation.Tests will be used for unit tests for Services.Impmentnation layer
- Services.Entities.Tests will be used for unit tests for Services.Entities layer
- One test file per class
- Do NOT mix multiple classes in one test file
- File name must exactly match the class name (case-sensitive) + "Tests", Test file names MUST follow this format:
<ClassName>Tests
- Keep test file in the corresponding folder structure if possible
- All dependencies MUST be mocked
- NEVER use real implementations of executors, repositories, or services
- Verify only one responsibility per test
- Not depend on other tests or shared state

## Compiler / Warning Policy
- Files MUST NOT include unnecessary `using` statements.
- Only include `using` directives that are required for compilation.
- Redundant or unused `using` directives are NOT allowed.
- No warnings related to unused usings are allowed
- CI build must pass with:
    - Warning level: maximum strictness
    - Treat warnings as errors (if enabled in project)

## Token Efficiency Rules
- Do not restate or summarize the user's question before answering
- Answer directly and concisely
- Avoid unnecessary introductions or conclusions
- Do not explain obvious steps unless requested
- Keep responses minimal but complete
- Prefer short code examples over long explanations
- Avoid repeating information already present in the conversation

