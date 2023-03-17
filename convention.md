# Contribution convention
## Contribution steps
1. You must be assigned to an issue you want to resolve
2. Do the fork from the updated "main" branch locally
3. All necessary changes must be done to the new branch
4. Push a new branch to the repository (it will be created there and set as the origin for the local one)
5. Make a Pull request
6. Link the issue related to this PR
7. Make the request for code review
8. If you are allowed to marge your branch with main, choose the option with squashing commits. Describe correctly all changes according to the commit convention described below.
9. Ensure that the link for this PR was placed in the commit name and the link for the issue in the commit footer
10. Attached issue will be closed automatically
11. The merged branch will be deleted automatically

## Branching
**main:** it's the main branch with production-ready code

**[example-name-branch]:*** new branch must be forked from "main" for further development

*\* name must be:*
- *self-explained;*
- *in lowercase;*
- *words separated by dash "-";*
## Commits:
```
<type>[(optional scope)]: <subject> [opotional #pr]

*[optional body]

[optional footer]
```

\<first line\>: here we introduce the type from the defined options below, optionally specify a scope(domain), and shortly describe the changes in this commit
+ must be no longer than 72 symbols
+ subject - capitalized
+ if this is finally squashed commit with merging to the main branch, must contain reference to PR (ex. #45)
  #### Variants of types:
- **fix:** a commit of the type fix patches a bug in your codebase (this correlates with PATCH in Semantic Versioning)
- **feat:** a commit of the type feat introduces a new feature to the codebase (this correlates with MINOR in Semantic Versioning)
- **test:** changes on the test layer of the code
- **docs:** changes in the docs
- **ci:** changes in the CI process
- **refactor:** the code was refactored (no fixes, no new features)
- **build:** changes in build process
- **chore:** some routine or bureaucratic things for product support, keeping it updated and secured

**\<body\>:** description of all changes in the commit 
+ must be one empty line before body
+ each change starts from a new line with "\*" 
+ each paragraph must be capitalized

**\<footer\>:** is used to place related links (for ex. - related issues). Here could be placed some needed notes.
+ must be one empty line before footer
+ must be in lowercase

### Special marks:
**!:** [optional] placed after the commit type in case you want to pay team attention to this commit (for ex. - breaking changes)

**BREAKING CHANGE:** [optinal] introduces a breaking API change (correlating with MAJOR in Semantic Versioning). A BREAKING CHANGE can be part of commits of any type.
### Examples

### Other requeremets


---
#### Commit message with description and breaking change footer:
```
feat: allow provided config object to extend other configs
BREAKING CHANGE: "extends" key in config file is now used for extending other config files
```

---
#### Commit message with ! to draw attention to breaking change:
```
feat!: send an email to the customer when a product is shipped
```

---
#### Commit message with scope and ! to draw attention to breaking change:
```
feat(api)!: send an email to the customer when a product is shipped
```

---
#### Commit message with both ! and BREAKING CHANGE footer
```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

--- 
#### Commit message with no body
```
docs: correct spelling of CHANGELOG
```

---
#### Commit message with scope
```
feat(lang): add Polish language
```

---
#### Commit message with multi-paragraph body and multiple footers and links for PR and issue
```
fix: prevent racing of requests #36

* Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

* Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

iss: #123 (linked)
```

# Pull request
**[name]:** explain the reason it was created and shortly describe the issue it has to resolve
- name must start with a capital letter;
- must be linked to the issue that related with this PR
- must be requested code reviewers
- squash the commits before merging with main
