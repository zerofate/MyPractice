> Git 中有两种方式可以将其他分支的变化合并到另一分支上，一种是 merge，另一种就是 rebase。
>
> 1011更新：（理解）rebase 相当于重新基于 master 的最新 commit 来对分支上的每一次 commit 重新进行比对，比对后的 commit 将是一个新的 commit，而旧的 commit 将被舍弃，该 commit 会有一个新的 id，但 message 不会变。比如，执行 rebase master 的操作流程如下：
>
> 1. 执行 git rebase master
> 2. 经过第一步，当前的 HEAD 是脱离分支状态，进入一个 rebase 的单独工作区（个人理解），这个工具区保留分支上的所有 commit，但其基于的 commit 是 master 上最新的 commit。开始合并分支的第一条 commit 和 master 的最新 commit，如果发生冲突，需要进行解决，解决完执行 git add 来标识冲突被解决，全部冲突解决完后，生成一条新的 commit（即使没有冲突，原来的提交 id 也会改变），接着执行 git rebase --continue 继续进行 rebase，即第二条 commit 与新生成的 commit 的比对。如果我们不想处理某一次的冲突，可以使用 git rebase --skip 来忽略。如果 rebase 过程中，想要放弃，可以执行 git rebase --abort，这样当前的 HEAD 会回到分支上。
>
>

参考：

[Git 分支 - 变基](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)

merge 和 rebase 最终得到结果没有任何区别，不过使用 rebase 可以使提交历史更为整洁，最终合并的提交历史看上去就像是串行的一样（如果直接使用 merge，得到的提交历史是按日期排序的，这样就把分支中的 commit 拆散开了，而 rebase 是将原有次序应用到另一分支上）。一般我们使用 rebase 是为了向远程分支 push 时能保持提交历史的整洁，如向某人维护的项目贡献代码，这样项目的维护者也不再需要进行整合工作，只需要快速合并即可。

### 部分语法

#### git rebase --onto

```$ git rebase --onto [--onto <newbase>] [<upstream>] [<branch>]```

基于指定的  newbase 分支而不是 upstream 分支（创建 branch 的分支）对 branch 进行 rebase 操作。

比如：

![Rebasing a topic branch off another topic branch.](https://git-scm.com/book/en/v2/images/interesting-rebase-2.png)

执行 `$ git rebase --onto master server client` 后

![Rebasing a topic branch off another topic branch.](https://git-scm.com/book/en/v2/images/interesting-rebase-2.png)

#### 快速 rebase

```$ git rebase [<upstream>] [<branch>]```

将 upstream 分支 rebase 到 branch 上，而不需要切换到 branch 下。rabase 后即可直接 merge branch。

### 风险

「**不要对在你的仓库外有副本的分支执行变基。** 」如果你遵循这条金科玉律，就不会出差错。 否则，人民群众会仇恨你，你的朋友和家人也会嘲笑你，唾弃你。

变基操作的**实质是丢弃一些现有的提交，然后相应地新建一些内容一样但实际上不同的提交**。 如果你已经将提交推送至某个仓库，而其他人也已经从该仓库拉取提交并进行了后续工作，此时，如果你用 git rebase 命令重新整理了提交并再次推送，你的同伴因此将不得不再次将他们手头的工作与你的提交进行整合，如果接下来你还要拉取并整合他们修改过的提交，事情就会变得一团糟。

> 理解，rebase 实际会导致一些 commit 被丢弃，如果这些 commit 已被 push，并被其他人 pull 了下来的话，如果这时候改用 rebase 而回滚 merge 操作，将导致其他人在再次进行 pull 时合并混乱，在 log 中将看到重复的 commit 记录。



### log 里出现两条相同的 commit

[Git commits are duplicated in the same branch after doing a rebase](https://stackoverflow.com/questions/9264314/git-commits-are-duplicated-in-the-same-branch-after-doing-a-rebase)

使用 rebase 要记住：**never rebase commits that have ever existed anywhere but your local repository**

> “相同”其实并不准确，实际是两条不同的 commit，一个是 rebase 前，一个是 rebase 后。他们出现的原因是该 commit 在 rebase 前已经 push，而 rebase 会产生一条新的 commit， rebase 后的 push 里并不会将该 commit 删除，所以就导致了两条“重复”的 commit。更具体的分析看上面的链接。