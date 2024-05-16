# Commit Messages ![Commit Messages](../assets/icons/git-commit.svg){: width="6%"}  

Using prefixes in commit messages is a common practice in many development workflows to categorize the nature of the commit. This helps in understanding the purpose of the commit at a glance, and can be particularly useful when generating changelogs, reviewing commits, or managing releases. Here are some commonly used prefixes:

1. **feat:** A new feature for the user.  
Example: feat: add user profile page

2. **fix**: A bug fix.  
Example: fix: resolve issue with login validation  

3. **docs**: Changes to documentation.  
Example: docs: update README with new setup instructions  

4. **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc.).  
Example: style: format code with Prettier  

5. **refactor**: A code change that neither fixes a bug nor adds a feature.  
Example: refactor: improve performance of data processing  

6. **perf**: A code change that improves performance.  
Example: perf: optimize image loading  

7. **test**: Adding missing tests or correcting existing tests.  
Example: test: add unit tests for UserService  

8. **build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm).  
Example: build: update webpack configuration  

9. **ci**: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs).  
Example: ci: add GitHub Actions for automated testing  

10. **chore**: Other changes that don’t modify src or test files (example scopes: updating dependencies).  
Example: chore: update project dependencies  

11. **revert**: Reverts a previous commit.  
Example: revert: revert commit 1234abcd  

12. **hotfix**: A critical fix that needs to be deployed immediately.  
Example: hotfix: patch security vulnerability  

These prefixes help maintainers and collaborators quickly understand the intent and scope of changes. They are especially useful when combined with a tool like Conventional Commits, which enforces a standard format for commit messages. This can also assist in automating release notes and versioning using tools like semantic-release.

##### Citations
<span style="font-size:small; color:grey;">
OpenAI. (2024). ChatGPT (GPT-4o) [Large language model].
</span>
