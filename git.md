# Rebase feature with sprint branch
- git fetch
- git checkout _sprint_
- git pull
- git checkout _feature_
- _git stash (facultatif)_
- git pull
- git rebase sprint
(git rebase --skip for unncessary commits)
- _git reset IdDuCommitSprint15 (facultatif)_
- _git stash apply (facultatif)_
- git pull
- git push

# Revert un commit
- git revert {id_commit}
- git pull
- git push

# Merging
- Resolve conflicts manually
- git add <files>
- git commit -m 'Merging files'

