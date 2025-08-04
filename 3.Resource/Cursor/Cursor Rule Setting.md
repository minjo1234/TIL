

---

description: QA Test Creation Rules and Guidelines
globs: ["qa/**/*.ts"]
alwaysApply: true

---

# QA Test Creation Rules

## Element Selection Rules

- ALWAYS use ID attributes as the primary selector method
- Example: `await page.click('#specificId')`
- Only use alternative selectors if ID is absolutely unavailable

## Code Organization

1. Utility Pages (DO NOT MODIFY)
- abstractPage.ts
- pageFactory.ts
- helpers/*.ts
These are core infrastructure files and should not be modified without team review.

1. Variable Management
- Global/Common variables → configs/data.ts
- Page-specific variables → Define in respective page objects
- Test-specific variables → Define within test files

1. Test Case Structure

```typescript

describe('[Feature Name]', () => {
customTest('[Category] [Feature] [Scenario Description]', async ({
pageObjects,

}) => {

await customStep("1. Step Description", async () => {

// Implementation

})
})
})
```

  

## Best Practices

1. Page Object Pattern
- Each page should have its own page object class

- Extend abstractPage.ts

- Keep page-specific selectors and methods within the page object

  

2. Reference Existing Tests

- Check similar test cases in the same domain

- Follow established patterns and conventions

- Maintain consistency with existing test structure

  

3. Variable Naming Conventions

- Use descriptive names that indicate purpose

- Follow camelCase for variables and methods

- Use PascalCase for class names

  

## Directory Structure

```

qa/

├── configs/ # Global configurations

│ ├── data.ts # Common variables

│ └── labels.ts # UI text/labels

├── pages/ # Page objects

├── helpers/ # Utility functions

├── fixtures/ # Test fixtures

└── tests/ # Test cases

```

  

## Code Review Requirements

- Elements are selected using IDs

- Common variables are in data.ts

- Page-specific variables are in page objects

- Test follows existing patterns

- No modifications to utility pages