# Git
## Rebase feature with sprint branch
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
- git push --force

## Revert un commit
- git revert {id_commit}
- git pull
- git push

## Merging
- Resolve conflicts manually
- git add _files_
- git commit -m 'Merging files'

## Squashing
Solution 1 : choisir le parent
- git merge-base _feature-branch_ _base-branch_ : donne l'id du commit parent
- git rebase -i _id-du-commit-parent_

Solution 2 : reprendre les X derniers commits
- git rebase -i HEAD~X

Dans tous les cas : 
- Entre en mode interactif, indiquer **pick** pour les commits à conserver et **squash** pour merger dans le commit précédent
- Quitter l'éditeur et enregistrer le nouveau message de commit
- git push --force

https://www.ekino.com/articles/comment-squasher-efficacement-ses-commits-avec-git

## Encryption avec Blackbox

TODO : dérouler le tuto https://www.man42.net/blog/2016/12/git-blackbox/

## Ressources

- Tooltip des erreurs : https://medium.com/@i_AnkurBiswas/common-git-mistakes-and-how-to-fix-them-10184cd5fa77
