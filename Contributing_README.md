# Contributing guidelines

### Workflow

We use a feature branch style git workflow where the main branch is protected and is only to contain a working version of the code. Branches are created as per their particular 'type' described below. More can be read about feature branching workflow here: <https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow>

### Branch naming conventions

The following branch naming convention must be followed. Any PR not in compliance will be denied. The naming convention going is as follows:

<name_of_author>/<branch_type>/<description_of_branch>

The following is a list of possible branch types:

- feature
- testing
- bugfix
- hotfix
- documentation

### Branching etiquette

- Branches must implement/change only a single feature. Changes related to that feature across different layers of code is acceptable.
- If you discover a bug unrelated to the feature you are working on, switch back to master, make a branch to fix the bug, then make a PR to merge that Bugfix. Chances are you aren't the only one experiencing the bug. You may rebase your development branch off the Bugfix branch.
- Branches that do not describe what they are changing will not be accepted.

### Issue format/styling standards

Every issue must have:

- At least one associated label
- A priority
- A difficulty
- A 'type'
- **A proper description**

Issues that have been started (moved from TODO) must have the following:

- An assignee
- An associated branch (if the item is not in 'TODO'. Obvious exceptions if the task cannot be related to a repo)
- A start date (the latest work shall begin on this)
- An End data (estimated)

#### Issue Template

```@md
## Description:

## Deliverables
- [ ] 

## Resources
- 

```

### Commit standards

- Use imperative mode in subject line. Think: If applied, this commit will ______ )
- Squash together commits that dont 'flow' or make sense, using an interactive rebase.

### Code styling

- All code files in this organization - relating to the ExAlta3 mission and onward - must follow a particular coding format and style. An automatic workflow action will test your code against theses standards automatically upon any request to merge with main.
- For Python: It is suggested to install a pylint linter extension in your IDE, to write code that follows these standards as you go.
- For C/C++: It is suggested to intsall a clang linter extension in your IDE, to write code that follows these standards as you go.

### Copying code

- Be sure to included referrences to code that is not your original work in order to prevent plagarism. Referencing code may also help members find information that may be useful to them.

### Copyright

- Ensure that every source file written has associated 'author' and 'copyright' metadata included in the file (for now it is found in the bottom, two lines after all code).
- Because these items will exist in every source file, style checkers like pylint must be told explicitly told to ignore them otherwise your code will fail style tests
- The following is an example template for the copyright to be added to ALL source files written by contributing members:

#### Copyright template

    Copyright 2023 [Your name here]
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
