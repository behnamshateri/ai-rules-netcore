This file provides guidance to any agent when working with code in this repository.

## Common Development Commands
- Build: `dotnet build` (targets .NET 8.0 via Directory.Build.props)
- Lint: Supported through analyzers configured in Directory.Build.props (Sonar, StyleCop)
- Test: `dotnet test` (includes unit/acceptance tests per test project structure)
- Run tests directly: Use `dotnet test <test-project>` (e.g., `dotnet test Financing.WebApi.Tests.Share`)

## Code Architecture Overview
1. **Core Modules**
    - `Financing.WebApi`: Primary API handling dispensation logic, including third-party integrations (Vektis, DAC)
    - `Financing.BL`: Business logic services (e.g., `Dispense.Financing` module under review for new API migration)
    - `Financing.Data`: Persistence layer (contains DbMigrations and DataAccessContext)

## Modern C# Rules

- Prefer modern C# language features over older syntax when supported
- Use the most concise and readable syntax available in the current .NET/C# version
- Refactor outdated syntax to modern alternatives in modified code when it improves readability
- Avoid unnecessary verbose syntax

## Explicit Type Declaration Rules

- Always use explicit type declarations instead of `var`
- `var` is only allowed for anonymous types
- Do not use `var` for local variables, foreach variables, using statements, or LINQ query results when the type can be expressed explicitly
- When modifying existing code that uses `var`, replace it with the explicit type when practical

## Formatting Rules

- Files MUST NOT contain trailing whitespace
- Remove trailing spaces from all modified lines before completing the task
- Preserve consistent file formatting and indentation
- Do not introduce unnecessary blank lines
- Ensure edited files end with a single newline
-
## Unit tests rules
- Unit tests should be written for all code paths
- Always use `Arrange-Act-Assert` pattern for unit tests
- Dont use `using var` in unit tests
- Dont use comments in unit tests
- Use fluent assertions for unit tests
- Services.Impmentnation.Tests will be used for unit tests for Services.Impmentnation layer
- Services.Entities.Tests will be used for unit tests for Services.Entities layer
- One test file per class
- Always use `EnumValidator.Validate(...)` for enum validation.
- Do not use `Enum.IsDefined(...)` directly.
- Unit tests for invalid enum values must verify `ValueNotSupportedException`.
- Do NOT mix multiple classes in one test file
- File name must exactly match the class name (case-sensitive) + "Tests", Test file names MUST follow this format:
  <ClassName>Tests
- Keep test file in the corresponding folder structure if possible
- All dependencies MUST be mocked
- NEVER use real implementations of executors, repositories, or services
- Verify only one responsibility per test
- Not depend on other tests or shared state
- Mock fields in test classes MUST end with `Mock`
- Mock field names MUST clearly describe the mocked dependency
- When writing chained method calls in C# tests, place each chained method on a new line.
```csharp
await _organizationsApiClientMock.DebtorCompaniesClient
    .Received(1)
    .GetDebtorCompanyByIdAsync(
        Arg.Is<Guid>(x => x == _debtorCompanyId),
        Arg.Any<GetDebtorCompanyByIdQueryParameters>());
```
- Use underscore-prefixed private field naming convention
  Examples:

```csharp
private IQueryHandler<GetPatientsActiveMandateOfOrganizationQuery, ICollection<Mandate>>
    _getPatientsActiveMandateOfOrganizationQueryHandlerMock;

private IObjectCreator<OrganizationPeopleContactInfo, OrganizationPeopleContactInfoCreatorInput>
    _organizationPeopleContactInfoCreatorMock;

private IAfasDebtorItemCreatorStrategy
    _afasDebtorItemCreatorStrategyMock;
```

- If multiple mocks exist for the same dependency type, append numeric suffixes

Example:

```csharp
private IService _serviceMock1;
private IService _serviceMock2;
```
- Do NOT only verify exception type, always validate exception properties and payload
- Please don’t run tests unless explicitly requested. If changes affect tests, only ensure the build passes without errors

## Unit test naming convention

- Every test name MUST strictly follow:
    ```csharp
        <MethodName>_<Condition>_<ExpectedBehavior>
    ```
- Test names MUST contain exactly two underscores separating exactly three sections
- Names with fewer or more sections are not allowed


### Invocation verification

- `...ShouldBeCalled`
- `...ShouldNotBeCalled`

Examples:

```csharp
HandleAsync_CommandIsValid_MapperShouldBeCalled
HandleAsync_CommandIsValid_UpsertDispenseAsBillableItemCommandHandlerShouldBeCalled
HandleAsync_CommandIsInvalid_MapperShouldNotBeCalled
```

### Exception verification

- `...ShouldBeThrown`
- `...ShouldNotBeThrown`

Examples:

```csharp
HandleAsync_CommandIsInvalid_ValidationExceptionShouldBeThrown
HandleAsync_CommandIsValid_ExceptionShouldNotBeThrown
```

## Code Review Rules
- Review and analyze code as a senior software engineer with strong experience in architecture, scalability, maintainability, and enterprise systems.
- Consider business impact, domain requirements, and real-world production scenarios during implementation and code review.
- Prioritize correctness, reliability, maintainability, security, and long-term sustainability over unnecessary optimizations or stylistic preferences.
- Evaluate both technical design and business logic correctness.
- Consider edge cases, failure scenarios, concurrency issues, and production risks.
- Validate that the implementation aligns with existing architecture and domain conventions.
- Prefer pragmatic solutions over over-engineering.
- Think beyond compilation success; evaluate operational impact, readability, extensibility, and future maintenance cost.

## Planning & Execution Rules

- Before making any code changes, first analyze the task and create an implementation plan
- Present the plan to the user and wait for explicit approval
- Do not modify any files, generate code, or execute commands until approval is received
- After approval, execute the agreed plan
- If the scope changes during implementation, stop and request approval for the updated plan


## Compiler / Warning Policy
- Files MUST NOT include unnecessary `using` statements.
- Only include `using` directives that are required for compilation.
- Remove unused `using` directives from all modified files
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

## Skill routing (IMPORTANT)
When a task matches one of these, load the skill:

| Task            | Skill path                    |
| Review a commit | `./skills/review-policy.md` |