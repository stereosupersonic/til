# Resolve Merge conflicts

## steps

```
git checkout master

git pull origin

git checkout branch_with_conflicts

git merge master

# resolve conflicts example structure.sql
git checkout origin/master db/structure.sql
bin/rake db:reset
bin rake db:migrate

git add .

git commit -m "Resolved merge conflict"

git push origin branch_with_conflicts
```
