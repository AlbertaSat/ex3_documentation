# Code Reviews

## What is a code review?
When you, or another team member wants add changes to an AlbertaSat repository they will go through a process defined by the (contributing guideline section)[Contributing_README.md]. This typically involves creating a branch, making changes, making a pull request, code review, then the reviewer either asks for changes to be made or approves the pull request. After the pull request is approved the code can be merged to main, or additional changes can be made. In this documentation we will go over guidelines for reviewing pull requests.

## How should a pull request look like?
__This section we will go over to how write a proper pull request that allows code reviewers to quickly and efficiently review code.__\
\
The following are some general rules of what a pull request should look like:\
- Change the default pull request name from the branch name to a descriptive name summarizes the changes you want to make.
- Add a useful description that includes the following:
    - The issue number linked to the pull request.
    - Any dependent pull requests in a different repository that should be reviewed first.
    - Describe the changes you made and how the changes you made solve the root issue.
    - If neccesary, clearly state any feedback you are looking for with a mention to the person who can help with feedback.
- If your pull request is still a work in progress, prefix the name of the pull request with "[WIP]".

## How should a pull request be reviewed?
__This section we will go over to how review a pull request.__\
\
The following are some general rules of how a reviewer should review a pull request:\
- If the PR is labelled as "WIP" then it should not be approved.
- Thoroughly go all changes made and if neccesary leave feedback.
- When leaving feed back try to be as specific as possible (Comment with the specific code line, and the requested change).
- Checkout the branch on your machine and test to ensure it does not break anything and implements the feature as intended.
- When requesting changes, be specifc about what you want changed (comment or propose a modified code block or line).
- Adhere to definitions of pull request approval, request for changes, and comments found in definition section.
- After the pull request has been merged (by either reviewer or creator of the pull request) the corresponding branch should be deleted and the pull request should be closed.

## Definitions

__Approve__: A pull request should only be approved after the reviewer has completed the following:
- reviewer has reviewed all code
- reviewer has tested code by checking out branch
- reviewer has confirmed the pull request implements the intended feature
- the pull request is not marked as in progress
- the pull request does not break any existing features
- creator of pull request has confirmed it is ready to be merged\
\
In summation, the pull request can only be marked as approved once it is ready to be merged with main. If any changes or feedback is given, the changes should be implemented and the creator of the pull request should re-request a review.

__Request for Changes__: A pull request can be reviewed and the reviewer can request changes, all changes should be resolved (fixed or ruled as not neccesary) before being re-reviewed. The reviewer should do their best to be specific about what changes should be made and if neccesary, explain how to implement them.


__Comment__: A pull request can be reviewed by leaving a comment which is general feedback for the creator can implement. After the creator of the pull request has resolved the feed back they can re-request a review. Although the feed back is general, the reviewer should try and be as helpful as possible in their feedback to help resolve the issue.

