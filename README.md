# Development Guidelines

Welcome to our development guidelines! These principles are designed to streamline our development process, enhance code quality, and maintain consistency across our projects. Please ensure you familiarize yourself with these guidelines and adhere to them throughout the development lifecycle.

# Programming Principles

## Write Pure Functions

Functions should produce the same output for the same input, avoiding side effects.

Example:

```elixir
# Good
defmodule Math do
  def add(a, b) do
    a + b
  end
end


# Bad (with side effects)
defmodule MathWithSideEffects do
  @total 0

  def add(a, b) do
    @total = a + b
    @total
  end
end
```

## Immutability by Convention

Immutable data structures prevent unintended mutations.

Example:

```elixir

# Good
immutable_list = [1, 2, 3]

# Bad (mutable list)
mutable_list = [1, 2, 3] |> List.delete_at(0)
```

## Functional Error Handling

Utilize exceptions or error objects for error handling.

Example:

```elixir
try do
  result = operation()
catch
  error -> Logger.error("Error occurred: #{inspect(error)}")
end
```

# Database Design

## Normalization Based on Rate of Change

Organize data into tables based on the frequency of changes.

Example:

```sql
CREATE TABLE rarely_changing_data (
    ...
);

CREATE TABLE frequently_changing_data (
    ...
);
```

## Never Store Derived Values

Computed data should be derived from materialized views.

Example:

```sql
CREATE MATERIALIZED VIEW monthly_sales AS
SELECT DATE_TRUNC('month', created_at) AS month, SUM(amount) AS total_sales
FROM sales
GROUP BY month;
```

# Architectural Patterns

## Event-Driven Architecture

Microservices react to events without direct communication.

## Realtime Architecture

Utilize websockets for real-time communication between frontend, backend, and database.

## Hexagonal Architecture

Separate core logic from external systems using ports-and-adapters.

# Code Development Practices

## Feature Flagging

Toggle features without code deployment using configuration flags.

## Avoid Loops

Prefer functional programming techniques for data iteration.

## Static Code Analysis and Linters

Ensure code quality and consistency through automated tools.

## Automated Unit Testing

Write unit tests to validate expected behavior of new code.

## No Reads Queries For Write Queries

Avoid network calls by completing logic in the database with a single query.

# API Design

## Versioning

Version APIs to maintain backward compatibility.

## Consistent Pluralization

Use consistent pluralization for resource endpoints.  (/post vs /posts)

## Appropriate HTTP Methods

Utilize appropriate HTTP methods for different actions. (do not use GET for everything)

## Test and Find Load Time

Ensure API responses are fast, ideally under 0.5 seconds.

## Use Caching, Compression, and CDNs

Optimize API performance with caching, compression, and CDNs.

## Security Measures

Implement HTTPS and authorization schemes for security.

# Code Management

## API Documentation

Keep API documentation current with tools like Postman, Swagger or Bruno.

## Architectural and Data Flow Diagrams

Document architectural and data flow diagrams for clarity.

## Code Comments

Explain the rationale ("why") rather than the mechanics ("what") in comments.

## Demo Videos

Record demo videos of the specific UI section or page when creating PRs, using screen recording tools like [Loom](https://www.loom.com/) or [Screenity](https://github.com/alyssaxuu/screenity), in order to understand the changes for the frontend. - Credits to Aditya Rawat for the idea

## Issue Tracking and Daily Updates

Use issue trackers for tasks and provide daily updates on progress.

# Additional Rules

## Managing Technical Backlog

When working on open issues or tasks, document any problems faced and their respective solutions by commenting on the corresponding GitHub issue. This helps in managing the technical backlog and serves as a reference for future work on similar issues.

## Detailed Task Management

Create detailed issues for every task with comprehensive sub-todos outlining your plan and a clear title indicating the objective.

Example Issue:

- Title: Implement User Authentication
- Description:
 - [ ] Research best authentication practices
 - [ ] Choose authentication library
 - [ ] Implement authentication endpoints
 - [ ] Write unit tests
 - [ ] Update API documentation

## Conventional Commits

Follow the conventional commits pattern for commit messages. Refer to [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) for guidelines.

Example Commit:

```
feat(authentication): implement user login endpoint

This commit adds the /login endpoint for user authentication.
```

## Atomic Commits
Break changes into atomic commits for better tracking. Refer to [Atomic Git Commits](https://www.aleksandrhovhannisyan.com/blog/atomic-git-commits) for guidance.

Example Atomic Commits:

1. Separate commits for adding new feature, fixing bug, and refactoring.
2. Each commit should represent a single logical change.


## Collaborative Code Reviews

Conduct thorough reviews with constructive feedback, focusing on improving code quality and fostering collaboration. Avoid blaming and instead offer suggestions for improvement.

Example Review Comment:

```
👍 Great work overall! Just one suggestion:
In line 42, let's refactor this function for better readability.
```

## Branching Strategy
Adopt a branching strategy with master and dev branches. Create separate feature branches for new features or bug fixes.

Example Branching:

- `master`: Represents the stable production-ready code.
- `dev`: Integration branch for ongoing development.
- `feature/authentication`: Feature branch for implementing authentication.
