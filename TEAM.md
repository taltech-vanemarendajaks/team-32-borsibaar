# Team 32

## Team name
Team 32

## Members
- Anastasija Selevjorstova (asyase)
- Joosep Lepik (jeesop45)
- Renet Rämman (RenetRamman)
- Tiina Kondio (tkondio)
- Vaire Riiet (Vaire444)

## Mentor
Riina Muld

## Workflow
- All changes are made in separate branches
- Code review is required before merging
- Merges into the main branch are done only after approval

## Merge strategies

### Used merge strategies
We used the following merge strategies during the project:

- **Merge commit**
- **Squash merge**
- **Rebase merge**

### Why we chose them
We decided to try out different merge strategies to better understand how they work and what their advantages and disadvantages are.

- **Merge commit** was useful for preserving the full branch history.
- **Rebase merge** helped keep a linear commit history.
- **Squash merge** combined all commits from a feature branch into one clean commit.

Overall, we found **squash merge** to be the best option, because it is safe and keeps the main branch history clean without unnecessary intermediate commits.

### Problems encountered
One issue we encountered was related to **merge conflicts**.

After resolving merge conflicts manually, we were sometimes unable to use **rebase merge**. In those situations, GitHub only allowed **squash merge** or **merge commit**.

This happened because rebasing requires a clean and conflict-free commit history. When conflicts are resolved through a normal merge, the branch history can no longer be rebased automatically, so GitHub disables the rebase option.

