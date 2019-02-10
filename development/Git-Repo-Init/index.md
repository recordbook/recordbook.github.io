---
layout: post
title:  "Git Repository Reset"
subtitle: "Git 저장소 초기화"
date:   2019-02-04 14:37:00
type: "Git"
development: true
text: true
author: "Choi corder"
---


git의 Repository를 초기화 하여 히스토리 부분을 다 날리는 방법은 아래와 같다.

# 1번째 방법
```
# Check out to a temporary branch:
git checkout --orphan TEMP_BRANCH

# Add all the files:
git add -A

# Commit the changes:
git commit -am "Initial commit"

# Delete the old branch:
git branch -D master

# Rename the temporary branch to master:
git branch -m master

# Finally, force update to our repository:
git push -f origin master
```


# 2번째 방법
```
# Clone the project, e.g. `myproject` is my project repository:
git clone https://github/heiswayi/myproject.git

# Since all of the commits history are in the `.git` folder, we have to remove it:
cd myproject

# And delete the `.git` folder:
git rm -rf .git

# Now, re-initialize the repository:
git init
git remote add origin https://github.com/heiswayi/myproject.git
git remote -v

# Add all the files and commit the changes:
git add --all
git commit -am "Initial commit"

# Force push update to the master branch of our project repository:
git push -f origin master
```

## 두 방법 모두 마지막 부분에서 자격 증명을 요구할 수 있다.