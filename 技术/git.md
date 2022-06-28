# git

## 踩坑记录

### 提交仓库时报错:

> ```bash
> On branch main
> Your branch is up to date with 'origin/main'.
> nothing to commit, working tree clean
> ```
>
> 

#### 原因: 

版本分支的问题

#### 解决办法

1. 新建一个分支

    `git branch newbranch`

2. 检查分支是否创建成功

    `git branch`

    星号(*),代表当前工作的分支

3. 切换到新的分支

    `git checkout newbranch `

4. 将新的改动提交到新的分支上

    `git add .`

    `git commit -m "comment"`

5. 检查是否成功

    `git status`

6. 切换到主分支

    `git checkout main`

7. 将新分支提交的改动合并到主分支上

    `git merge newbranch`

8. push代码

    `git push -u origin main`

9. 最后可以删除这个分支

    `git branch -D newbrnch`

