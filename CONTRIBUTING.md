# Contributing to NDU NAPSS E-Library

## Code of Conduct

We are committed to providing a welcoming and inclusive environment. All contributors are expected to:
- Be respectful and professional
- Provide constructive feedback
- Help others learn and grow
- Report issues constructively

---

## Getting Started

### 1. Fork & Clone
```bash
git clone https://github.com/your-username/ndu-napss-e-library.git
cd ndu-napss-e-library
git remote add upstream https://github.com/ndu-napss-e-library/ndu-napss-e-library.git
```

### 2. Create Feature Branch
```bash
git checkout -b feature/your-feature-name
```

### 3. Setup Development Environment
Follow [SETUP.md](./docs/SETUP.md) in the docs folder.

---

## Commit Convention

### Format
```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type
- **feat**: New feature
- **fix**: Bug fix
- **docs**: Documentation
- **style**: Code style (formatting, semicolons, etc.)
- **refactor**: Code refactor
- **perf**: Performance improvement
- **test**: Tests
- **chore**: Build, dependencies

### Examples
```
feat(auth): Add two-factor authentication
fix(books): Fix PDF upload validation error
docs(api): Update authentication endpoints
test(users): Add user registration tests
```

---

## Pull Request Process

### 1. Before Submitting
```bash
# Run linter
npm run lint

# Format code
npm run format

# Run tests
npm test

# Check coverage
npm run coverage
```

### 2. Create PR
- Use descriptive title
- Reference related issues (#123)
- Describe changes clearly
- Include screenshots if UI changes

### 3. PR Template
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation

## Related Issues
Closes #123

## Testing
How to test these changes

## Screenshots (if applicable)
Add screenshots

## Checklist
- [ ] Tests pass
- [ ] Code follows style guide
- [ ] Documentation updated
- [ ] No breaking changes
```

### 4. Approval & Merge
- Wait for code review
- Address feedback
- Squash commits if needed
- Merge to main

---

## Development Workflow

### Feature Development
```bash
# Create feature branch from main
git checkout -b feature/feature-name

# Make changes
# Commit regularly
git commit -m "feat: Add feature"

# Push to your fork
git push origin feature/feature-name

# Create pull request
# Wait for review and merge
```

### Bug Fixing
```bash
# Create fix branch
git checkout -b fix/bug-name

# Fix the bug
# Write tests to prevent regression

# Commit
git commit -m "fix(module): Fix bug description"

# Push and create PR
```

---

## Code Style Guide

### JavaScript/React
```javascript
// Use const/let, not var
const name = 'value';

// Use arrow functions
const greet = (name) => {
  return `Hello, ${name}`;
};

// Use template literals
const message = `Hello, ${name}`;

// Use async/await
const fetchData = async () => {
  try {
    const response = await fetch('/api/data');
    return response.json();
  } catch (error) {
    console.error(error);
  }
};
```

### Component Structure
```javascript
// React component example
import React, { useState } from 'react';

const MyComponent = ({ prop1, prop2 }) => {
  const [state, setState] = useState(null);

  const handleClick = () => {
    // Handle click
  };

  return (
    <div>
      {/* JSX here */}
    </div>
  );
};

export default MyComponent;
```

### File Organization
- One component per file
- Use meaningful file names
- Group related files
- Keep components under 300 lines

### Naming Convention
- Components: PascalCase (MyComponent.jsx)
- Functions: camelCase (myFunction)
- Constants: UPPER_SNAKE_CASE (API_URL)
- Files: kebab-case (my-component.jsx)

---

## Testing Requirements

### Unit Tests
```javascript
describe('MyComponent', () => {
  it('should render correctly', () => {
    const { getByText } = render(<MyComponent />);
    expect(getByText('Expected Text')).toBeInTheDocument();
  });
});
```

### Test Coverage
- Minimum 80% coverage
- All functions tested
- Edge cases covered
- Error scenarios tested

### Running Tests
```bash
# Run all tests
npm test

# Run with coverage
npm run coverage

# Run specific test
npm test -- myComponent.test.js

# Watch mode
npm test -- --watch
```

---

## Documentation Requirements

### Code Comments
```javascript
// Use JSDoc for complex functions
/**
 * Fetch books from API
 * @param {number} page - Page number
 * @param {number} limit - Items per page
 * @returns {Promise<Array>} Books array
 */
const fetchBooks = async (page, limit) => {
  // Implementation
};
```

### Update Documentation
- Update README.md for major changes
- Update API.md for endpoint changes
- Add comments for complex logic
- Document breaking changes

---

## Issue Reporting

### Before Reporting
- Check if issue already exists
- Test with latest version
- Gather all information
- Include error messages

### Issue Template
```markdown
## Description
Clear description of the issue

## Reproduction Steps
1. Step 1
2. Step 2
3. Step 3

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- OS: Windows/Mac/Linux
- Node: version
- Browser: version

## Screenshots
Add if applicable
```

---

## Feature Requests

### Guidelines
- Describe the feature clearly
- Explain use case
- Provide examples
- Reference related issues

### Template
```markdown
## Feature Description
Clear description

## Use Case
Why this feature is needed

## Proposed Solution
How to implement

## Alternatives Considered
Other approaches
```

---

## Code Review Process

### What Reviewers Look For
- Code quality
- Test coverage
- Documentation
- Performance
- Security
- Consistency

### Response to Feedback
- Thank reviewer for feedback
- Ask questions if unclear
- Make requested changes
- Push updates
- Respond to all comments

---

## Helpful Resources

- [Setup Guide](./docs/SETUP.md)
- [API Documentation](./docs/API.md)
- [Database Schema](./docs/DATABASE.md)
- [Phase Details](./docs/PHASES.md)
- [Professional Guide](./docs/PROFESSIONAL_GUIDE.md)

---

## Getting Help

- **GitHub Issues**: Ask questions
- **GitHub Discussions**: Discuss ideas
- **Pull Request Comments**: Ask for clarification
- **Project Maintainers**: Contact team leads

---

## Merging Guidelines

### Requirements
- ✅ All tests pass
- ✅ Code review approved
- ✅ No conflicts
- ✅ Documentation updated
- ✅ Commits squashed (if needed)

### Process
1. Ensure all CI checks pass
2. Get approval from maintainer
3. Squash if multiple commits
4. Merge to main
5. Delete feature branch

---

## Release Process

### Version Numbering
Semantic Versioning: MAJOR.MINOR.PATCH
- MAJOR: Breaking changes
- MINOR: New features
- PATCH: Bug fixes

### Release Steps
1. Update version number
2. Update CHANGELOG
3. Create release notes
4. Tag release
5. Deploy to production

---

## Questions?

Feel free to ask in:
- GitHub Issues
- GitHub Discussions
- Project maintainers

Thank you for contributing! 🎉
