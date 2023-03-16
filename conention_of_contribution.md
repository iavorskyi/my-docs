# Contribution convention
## Contribution steps
1. You must be assigned to an issue you want to resolve
2. Do the fork from the updated "main" brunch locally
3. All necessary changes must be done to the new brunch
4. Push a new brunch to the repository (it will be created there and set as the origin for the local one)
5. Make a Pull request
6. Link the issue related to this PR
7. Make the request for code review
8. If you are allowed to marge your brunch with main, choose the option with squashing commits. Describe correctly all changes according to the commit convention described below.
9. Ensure that the link for this PR was placed in the commit name and the link for the issue in the commit footer
10. Attached issue will be closed automatically
11. The merged brunch will be deleted automatically

## Brunching
**main:** it's the main brunch with production-ready code

**[example-name-brunch]:*** new brunch must be forked from "main" for further development

*\* name must be:*
- *self-explained;*
- *in lowercase;*
- *words separated by dash "-";*
## Commits:
```
<type>[(optional scope)]: <description> [opotional #pr]

*[optional body]

[optional footer]
```

\<type\>:
- **fix:** a commit of the type fix patches a bug in your codebase (this correlates with PATCH in Semantic Versioning)
- **feat:** a commit of the type feat introduces a new feature to the codebase (this correlates with MINOR in Semantic Versioning)
- **test:** changes on the test layer of the code
- **docs:** changes in the docs
- **ci:** changes in the CI process
- **refactor:** the code was refactored (no fixes, no new features)
- **build:** changes in build process
- **chore:** some routine or bureaucratic things for product support, keeping it updated and secured

**\<body\>:** description of all changes in the commit. Each change starts from a new line with "\*" in lowercase

**\<footer\>:** is used to place related links (for ex. - related issues). Here could be placed some needed notes.

### Special marks:
**!:** [optional] placed after the commit type in case you want to pay team attention to this commit (for ex. - breaking changes)

**BREAKING CHANGE:** [optinal] introduces a breaking API change (correlating with MAJOR in Semantic Versioning). A BREAKING CHANGE can be part of commits of any type.
### Examples

---
#### Commit message with description and breaking change footer:
feat: allow provided config object to extend other configs
BREAKING CHANGE: \`extends\` key in config file is now used for extending other config files

---
#### Commit message with ! to draw attention to breaking change:
feat!: send an email to the customer when a product is shipped

---
#### Commit message with scope and ! to draw attention to breaking change:
feat(api)!: send an email to the customer when a product is shipped

---
#### Commit message with both ! and BREAKING CHANGE footer
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.

--- 
#### Commit message with no body
docs: correct spelling of CHANGELOG

---
#### Commit message with scope
feat(lang): add Polish language

---
#### Commit message with multi-paragraph body and multiple footers and links for PR and issue
fix: prevent racing of requests #36

* Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

* Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

iss: #123 (linked)

# Pull request
**[name]:** must explain the reason it was created and shortly describe the issue it has to resolve; must start with a capital letter;
