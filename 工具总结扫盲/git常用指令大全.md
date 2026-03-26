# Git 常用指令汇总（日常开发必备）
按**使用场景分类整理**，覆盖**本地操作、分支管理、远程同步、版本回退**等核心场景，新手直接复制使用即可。

---

## 一、初始配置（首次使用 Git 必执行）
配置用户名/邮箱（**全局生效**，所有仓库通用）
```bash
# 配置用户名
git config --global user.name "你的名字"
# 配置邮箱（和远程仓库邮箱一致）
git config --global user.email "你的邮箱"
```

基础配置指令
```bash
# 查看所有配置信息
git config --list
# 编辑全局配置文件
git config --global --edit
```

---

## 二、本地仓库基础操作
```bash
# 1. 初始化本地仓库（在项目文件夹执行）
git init

# 2. 克隆远程仓库到本地
git clone 远程仓库地址

# 3. 查看当前仓库状态（文件修改/新增/删除）
git status
```

---

## 三、工作区 → 暂存区 → 本地仓库（核心提交流程）
Git 三区域：工作区（写代码）→ 暂存区（临时保存）→ 本地仓库（永久提交）
```bash
# 1. 添加单个文件到暂存区
git add 文件名

# 2. 添加所有修改/新增文件到暂存区（最常用）
git add .

# 3. 提交暂存区内容到本地仓库（必须加备注）
git commit -m "提交说明：修复bug/新增功能等"

# 4. 一步完成 add + commit（仅适用于已跟踪的文件）
git commit -am "提交说明"

# 5. 查看工作区与暂存区的差异
git diff

# 6. 查看暂存区与本地仓库的差异
git diff --cached
```

---

## 四、分支管理（团队开发核心）
**默认主分支：main / master**
```bash
# 1. 查看所有本地分支
git branch

# 2. 查看所有分支（本地+远程）
git branch -a

# 3. 创建新分支
git branch 分支名

# 4. 切换分支
git switch 分支名  # 新版推荐
git checkout 分支名 # 旧版兼容

# 5. 创建并直接切换到新分支（最常用）
git switch -c 分支名
git checkout -b 分支名

# 6. 合并指定分支到当前分支
git merge 要合并的分支名

# 7. 删除本地分支（已合并）
git branch -d 分支名

# 8. 强制删除本地分支（未合并）
git branch -D 分支名

# 9. 重命名分支
git branch -m 新分支名
```

---

## 五、远程仓库操作（同步 GitHub/GitLab）
```bash
# 1. 关联本地仓库与远程仓库
git remote add origin 远程仓库地址

# 2. 查看远程仓库信息
git remote -v

# 3. 首次推送本地分支到远程（绑定关联）
git push -u origin 分支名

# 4. 推送本地代码到远程仓库（后续直接用）
git push

# 5. 拉取远程仓库最新代码到本地
git pull

# 6. 仅拉取远程代码（不自动合并）
git fetch

# 7. 移除远程仓库关联
git remote remove origin

# 8.自动绑定指令 （push 时自动设置远程分支）
git config --global push.autoSetupRemote true

```




---

## 六、版本回退与撤销（误操作救星）
```bash
# 1. 查看提交日志（简洁版）
git log --oneline

# 2. 回退到上一个版本（保留本地代码，仅撤销提交）
git reset --soft HEAD~1

# 3. 彻底回退到上一个版本（删除本地未提交代码，谨慎！）
git reset --hard HEAD~1

# 4. 回退到指定版本（commit-id 从 git log 中复制）
git reset --hard 提交ID

# 5. 撤销工作区的修改（恢复到最近一次提交状态）
git checkout -- 文件名

# 6. 撤销暂存区的文件（放回工作区）
git reset HEAD 文件名
```

---

## 七、标签管理（版本标记，如 v1.0）
```bash
# 1. 打标签（当前版本）
git tag v1.0

# 2. 查看所有标签
git tag

# 3. 推送单个标签到远程
git push origin v1.0

# 4. 推送所有标签到远程
git push origin --tags
```

---

## 八、暂存工作区（临时保存未完成代码）
切换分支前，若代码未写完不想提交，用 `stash` 暂存
```bash
# 1. 暂存当前修改
git stash

# 2. 查看所有暂存记录
git stash list

# 3. 恢复最近一次暂存，并删除该记录
git stash pop

# 4. 恢复最近一次暂存（保留记录）
git stash apply

# 5. 删除所有暂存记录
git stash clear
```

---

## 九、其他实用指令
```bash
# 1. 清理项目中未跟踪的文件/文件夹
git clean -fd

# 2. 取消合并（合并冲突时放弃合并）
git merge --abort

# 3. 查看指定指令的帮助文档
git help 指令名
```

---

### 总结
1. **日常开发流程**：`git add .` → `git commit -m` → `git push`
2. **团队协作核心**：分支创建/切换/合并（`git checkout -b` / `git merge`）
3. **误操作急救**：`git reset`（版本回退）、`git stash`（暂存代码）