# Branch Naming Conventions

### Sample Branch Names
- `prefix/branch-description-card#`
- `feature/user-authentication`
- `bugfix/fix-header-styling-40`
- `hotfix/security-patch`

### Basic Rules
- Lowercase and Hyphen-separated
- Alphanumeric Characters (a-z, 0-9)
- Descriptive

### Branch Prefixes
- **Bugfix**  
Branches used for fixing bugs  
`bugfix/`
- **Hotfix**   
Branches that are made directly from production branch to fix critical bugs in production environment  
`hotfix/`
- **Release**  
Branches created to prepare for a new release of the software. These branches typically include final testing and stabilization before a release is made.  
`release/verision_0.1.9-alpha`
- **Refactor**  
 Branches created to refactor code without changing its external behavior. This can include restructuring code for readability, performance improvements, or adherence to coding standards.  
`refactor/`
- **Documentation**  
Branches created for updating or adding documentation, such as README files, user guides, or API documentation.  
`doc/` or `documentation/`
- **Experiment**  
Branches created for experimental or exploratory development work. These branches are used for trying out new ideas or technologies without affecting the main codebase.  
`experiment/`  
- **Integration**  
Branches created for integrating changes from multiple developers or teams. These branches are often used in larger projects with multiple contributors to coordinate changes before merging into the main branch.  
`integration/`  
- **Test**  
Branches created specifically for testing purposes, such as running automated tests or conducting manual QA testing  
`test/`  
- **Chore**  
Branches created for miscellaneous tasks or housekeeping activities, such as updating dependencies, configuring build scripts, or cleaning up code.  
`chore/`  

### Card/Ticket Numbers (optional)
- Reference Trello Card Number or Ticket Numbers at end of branch name

##### Citations
<small>
- <a href="https://medium.com/@abhay.pixolo/naming-conventions-for-git-branches-a-cheatsheet-8549feca2534" target="_blank">Naming conventions for Git Branches — a Cheatsheet</a>
</small>