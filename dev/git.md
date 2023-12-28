# Git

## Docs
[Pro Git Book](https://git-scm.com/book/en/v2)  
[Writing good commit messages](https://www.freecodecamp.org/news/writing-good-commit-messages-a-practical-guide/)  

## Commit message convention

### Commit message
```
<type>(optional scope): short summary in imperative mood
# empty line
<optional body: what & why>
# empty line
<optional footer: breaking changes, issue/task reference>
```

### Commit Type
- **build**: Commits that affect build components, including build tools, CI pipeline, project dependencies, and project version  
- **feat**: Commits that add new features to the codebase  
- **fix**: Commits that address and resolve bugs in the code  
- **test**: Commits that add missing tests or correct existing tests to improve the code's test coverage  
- **refactor**: Commits that involve rewriting or restructuring the code without changing its behavior  
- **perf**: Special refactor commits that focus on improving performance  
- **style**: Commits, that do not affect the meaning (white-space, formatting, missing semi-colons, etc)  
- **docs**: Commits that only affect the project's documentation, such as updating README files or modifying comments  
- **chore**: Commits that encompass miscellaneous changes, such as modifying the .gitignore file or performing housekeeping tasks  
- **ops**: Commits that affect operational components like infrastructure, deployment processes, backup mechanisms, and recovery procedures

### Optional scope
Depends on specific project, but generally it should provide additional contextual information

Examples:
```
docs(lang): add CZ and SK translations
fix(user-api): return correct status code on unauthorized
build(release): version 1.2.3
```

### Optional footer
Breaking changes and references to issues should be at the end of body
```
feat(api-v2)!: orders endpoints returns different body

#YT-2345

BREAKING CHANGE: yada yada yada
```