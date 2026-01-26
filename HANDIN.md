
# Homework: Team Workflow with Git & GitHub - Documentation

# Pull Requests

All project changes were merged into the 'main' branch using GitHub pull requests

Links to pull requests:

PR #1 - Feature: team32-9-merge-conflict-2  
https://github.com/taltech-vanemarendajaks/team-32-borsibaar/pull/1

PR #2 - Feature: controller_refac  
https://github.com/taltech-vanemarendajaks/team-32-borsibaar/pull/2

PR #3 - Feature: team32-11-inventory-sorting  
https://github.com/taltech-vanemarendajaks/team-32-borsibaar/pull/3

PR #4 - Feature: team32-9-merge-conflict-3  
https://github.com/taltech-vanemarendajaks/team-32-borsibaar/pull/4

PR #5 - Feature: team32-12-public-health  
https://github.com/taltech-vanemarendajaks/team-32-borsibaar/pull/5

PR #6 - Feature: handin_file
https://github.com/taltech-vanemarendajaks/team-32-borsibaar/pull/6

## Merge Conflict Explanation

### Description of the conflict
An intentional merge conflict was created as part of the assignment.
Tiina and Vaire modified the page.tsx and edited the comments independently in their own feature branches without coordinating the changes.

When attempting to merge the second branch into `main`, Git detected conflicting changes and stopped the merge process.

### How the conflict was resolved
- The conflict was resolved **locally using the Git command line**
- The conflicting file was opened and the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) were manually reviewed
- The final version combined the correct and meaningful parts of changes
- After resolving the conflict, the file was added and committed
- The updated branch was pushed to GitHub and merged via a merge request

This ensured the project remained functional and the final result made sense.

## Team Members and Contributions

### Team Member 1
- **Name:** Tiina
- **Work done:**
  - Worked on a separate feature branch
  - Made multiple commits
  - Opened a pull request
  - Implemented feature: team32-9-merge-conflict-2 was merged using a **regular merge commit**. 	
  - Implemented feature: team32-9-merge-conflict-3 was merged using a **squash merge**. After resolving the merge conflict, merging via rebase was not allowed, so a squash was performed.
  - Participated in intentional merge conflict
  - Resolved merge conflicts
  - Participated in code reviews
  - Reviewed pull requests
  - Ensured repository hygiene (deleted branches, clean history)
  - Updated the TEAM.md file

### Team Member 2
- **Name:** Anastasija
- **Work done:**
  - Worked on a separate feature branch
  - Made multiple commits
  - Opened a pull request
  - Implemented feature: team32-11-inventory-sorting was merged using a **rebase merge**
  - Ensured repository hygiene (deleted branches, clean history)

### Team Member 3
- **Name:** Joosep
- **Work done:**
  - Worked on a separate feature branch
  - Made multiple commits
  - Opened a pull request
  - Implemented feature: team32-12-public-health was merged using a **regular merge commit**
  - Ensured repository hygiene (deleted branches, clean history)

### Team Member 4
- **Name:** Renet
- **Work done:**
  - Worked on a separate feature branch
  - Made multiple commits
  - Opened a pull request
  - Implemented feature: controller_refac was merged using a **regular merge commit**
  - Reviewed pull requests and left comments
  - Ensured repository hygiene (deleted branches, clean history)

### Team Member 5
- **Name:** Vaire
- **Work done:**
  - Created the main team repository
  - Created the TEAM.md file
  - Worked on a separate feature branch
  - Opened a pull request
  - Implemented feature: team32-9-merge-conflict-1 was merged using a **regular merge commit** without a PR.
  - Implemented feature; handn_file was merged using a **regular commit** 
  - Participated in intentional merge conflict
  - Resolved merge conflicts
  - Reviewed pull requests and left comments
  - Ensured repository hygiene (deleted branches, clean history)
  - Created the HANDIN.md file


## Summary

This assignment helped us practice:
- Working with Git from the command line
- Using feature branches and pull requests
- Resolving merge conflicts
- Reviewing code in GitHub
- Using different merge strategies (merge commit, squash, rebase)

All required steps were completed according to the assignment instructions.
