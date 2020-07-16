# Git使用

### 初始工作

* 初始化本地库

  > git init

* 设置签名

  > * 项目签名
  >
  >   git config user.name xxx
  >
  >   git config user.email xxx@xxx
  >
  >   查看：cat 本地库目录/.git/config
  >
  > * 系统签名
  >
  >   git config --global user.name xxx
  >
  >   git config --global user.email xxx@xxx
  >
  >   查看：cat ~/.gitconfig
  >
  >   ![image-20200408214946871](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200408214946871.png)
  >
  > * 就近原则：项目签名优先级更高

### 正式使用

#### 本地库操作

##### 基本操作

* 查看状态

  > git status

* 添加文件到暂存区

  > git add filename

* 移除暂存区内容

  > git rm --cached filename

* 撤销修改

  > git checkout -- filename

* 将暂存区提交到本地库

  > git commit filename
  >
  > git commit -m "Second commit: modify test.txt" test.txt
  >
  > git commit -a

* 将暂存区撤销提交

  > git reset HEAD filename

* 查看历史记录

  > git log : 完整地显示
  >
  > git log --oneline : 简洁地显示，且只显示当前版本之前地记录
  >
  > git log --pretty=oneline
  >
  >  
  >
  > git reflog : 在oneline地基础上，显示了HEAD指针，并且显示所有历史记录
  >
  > ![image-20200409211326864](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200409211326864.png)

* 版本移动

  > git reset --hard <索引号>
  >
  > ^ ：回退  HEAD^回退一个版本（n个^回退n步）
  >
  > ~ ：回退   HEAD~3 回退三步

* reset的三个参数对比

  > --soft : 不会影响暂存区和工作区，只在本地库移动HEAD指针
  >
  > --mixed : 在本地库移动HEAD指针，重置暂存区
  >
  > --hard(最常用) : 移动HEAD同时重置暂存区和工作区

* 比较文件差别

  > git diff filename：默认和暂存区比较
  >
  > git diff [历史版本指针] filename ：和历史记录比较
  >
  > git diff ：不带文件名比较所有文件

##### 分支

在新分支开发功能，失败直接舍弃分支即可，可以避免风险。

多部门同时进行，互不影响，提高效率

![image-20200409215020139](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200409215020139.png)

* 分支操作

  - git branch -v ：查看分支

  - git branch 分支名 ：创建分支

  - git checkout hot_fix ：切换分支

  - 合并分支

    >1. 切换到合并后保留的分支上
    >2. git merge hot_fix(被合并分支名)

  - 解决冲突

    > 1. 分支的表现：
    >
    > ![image-20200409220655231](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200409220655231.png)
    >
    > 2. 修改文件内容到合适的地步
    >
    > 3. ![image-20200409220807881](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200409220807881.png)
    >
    > 4. 标记合并
    >
    >    git add filename
    >
    >    ![image-20200409220941581](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200409220941581.png)
    >
    > 5. 完成合并
    >
    >    git commit (不能带文件名)

#### 远程库操作

##### 创建远程库

- 使用GitHub创建远程库，记录它的地址

##### 本地保存远程库地址

- git remote -v：查看远程库列表
- git remote add 库名 地址：添加新的远程库地址

##### 推送本地内容

- git push 库名 分支名：将本地分支推送到某个远程库，需要输入GitHub用户名和密码

  > git push origin branch:remote-branch [--force]

##### 从远程库拉取内容

- git clone 远程地址

  > 1. 将远程库整个拷贝到本地
  > 2. 完成本地库的初始化
  > 3. 创建origin远程库别名

- git fetch 库名 分支名：将远程库下载为新分支，但不影响工作区，需要执行merge

- git pull 库名 分支名：pull = fetch + merge

##### 邀请其它成员参与

![image-20200411213231188](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411213231188.png)

![image-20200411213246301](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411213246301.png)

##### 冲突处理

1. 两个以上用户同时push了新的修改
2. 后push的用户会失败
3. pull最新内容
4. 在本地处理冲突
5. 重新push

##### 跨团队协作（远程库间的操作）

​	**fork + pull request**

1. 团队外人员fork一份库

   ![image-20200411214643847](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411214643847.png)

2. 团队外人员将库clone到本地

3. 团队外人员做合适的开发

4. 团队外人员push到自己的远程库

5. 团队外人员发起pull request

   ![image-20200411214953370](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411214953370.png)

6. 团队内人员选择是否接受该request，或给提交者回复

   - 查看提交

   ![image-20200411215136557](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411215136557.png)

   - 审核代码

   ![image-20200411215314133](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411215314133.png)

   - 合并代码

   ![image-20200411215330712](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200411215330712.png)

   

