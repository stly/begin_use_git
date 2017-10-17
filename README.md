开发指南
========

说明
----

1. 如未作特殊说明，所有命令的执行环境为本地开发机。

2. 目前有两台服务器，分别为正式产品环境(以下简称production) 和预发布环境(以下简称staging) 。


Git, Gitlab 和 Gitflow
----------------------


### Git 使用

1. 廖雪峰Git[教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
2. Pro Git[教程](https://git-scm.com/book/zh/v2)

### 获取源码

1. 使用 Git 管理源码。获取源码:

    ```sh
    git clone https://gitee.com/zonton/rongtongteacher.git
    ```

2. 代码和文档可以在 [Gitee](https://gitee.com/zonton/rongtongteacher) 上查看。当有新功能需要上线时，首先请其他人在 Gitee 上 Review 代码。

3. 开发严格使用 [Gitflow](https://github.com/nvie/gitflow) 流程。

### Gitflow 流程

1. 首先请安装并设置好 [Gitflow](https://github.com/nvie/gitflow).

2. eclipse安装egit [EGit Download](http://www.eclipse.org/egit/download/) [EGit Guide](https://wiki.eclipse.org/EGit/User_Guide).

3. 开发新功能时，首先创建 feature 分支，分支命名规则为 yyyymmdd_username_featurename，如 20171009_yangjian_update_readme:

    ```sh
    git flow feature start 20171009_yangjian_update_readme
    ```

    该命令会自动创建并切换到分支 20171009_yangjian_update_readme, 请在此分支上开发。

4. 当功能开发完成后，确保本地单元测试通过，手工测试通过，代码在 [Gitee](https://gitee.com/zonton/rongtongteacher) 上经过其他人 review, 然后将代码合并到 develop 并 push 到服务器:

    ```sh
    # 此时在 feature/20171009_yangjian_update_readme 分支上，命令执行后会切换到 develop 分支上
    git flow feature finish 20171009_yangjian_update_readme
    # 此时在 develop 分支上
    git push
    ```

预发布及正式部署
----------------


1. 部署前保证所有测试通过, feature 已经 finish 并合并到 develop。

2. 创建并发布 release 分支. release 分支的规则为 yyyymmdd, 如：

    ```
    git flow release start 20171009
    git flow release publish 20171009
    ```

3. 将 release 分支部署到 staging 服务器：

    ```
    ```

4. 在 staging 上查看功能是否正常，如果有问题，直接在 release 分支上修改并 push.

5. 当确认 staging 上一切正常后 finish release 分支。如:

    ```
    git flow release finish 20171009
    git push --tags
    ```
    
    注意: release 分支在 finish 的过程中会建立 release tag, release tag 的格式为 yymmdd, 如 20190922.
    因为 finish release 分支时会将它分别合并到 master 和 develop, 并创建 tag, 所以切记要补全这三种提交信息，否则 finish 可能会中断！

6. 此时新增的功能已在 master 分支上。最后部署 master 分支到产品环境（请谨慎使用！）:

    ```
    ```

7. 在预发布及正式部署过程中，请时刻关注 [NewRelic](https://rpm.newrelic.com/accounts/1006650/applications) 各种监控指标的变化（尤其是异常）！

参考链接
--------

* [Gitflow Cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/)
