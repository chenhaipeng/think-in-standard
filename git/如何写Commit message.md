# 如何写Commit message

## 1. Commit message的作用

**（1）提供更多的历史信息，方便快速浏览**

 ```shell
$ git log <last tag> HEAD --pretty=format:%s
 ```

**（2）可以过滤某些commit（比如文档改动），便于快速查找信息**

```shell
$ git log <last release> HEAD --grep feature
```

**（3）可以直接从commit生成Change log**

Change Log 是发布新版本时，用来说明与上一个版本差异的文档，详见后文

![Changelog](http://www.ruanyifeng.com/blogimg/asset/2016/bg2016010603.png)

## 2. Commit message 的格式

每次提交，Commit message 都包括三个部分：Header和Body 。

```shell
<type>(<scope>): <subject>
// 空一行
<body>
```

其中，Header 是必需的，Body 可以省略。

不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

### 2.1 Header

Header部分只有一行，包括三个字段：`type`（比需）、`scope`（可选）和`subject`（比需）。

#### **（1）type**

`type`用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

如果`type`为`feat`和`fix`，则该 commit 将肯定出现在 Change log 之中。其他情况（`docs`、`chore`、`style`、`refactor`、`test`）由你决定，要不要放入 Change log，建议是不要。

#### **（2）scope**

`scope`用于标明本次提交对应的问题号，如jira上的问题号，格式为 `#问题号`。

#### **（3）subject**

`subject`是 commit 目的的简短描述，不超过50个字符。

- 以动词开头
- 结尾不加句号（。）或者句点（`.`）

### 2.2 Body

Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

> ```
> More detailed explanatory text, if necessary.  Wrap it to 
> about 72 characters or so. 
>
> Further paragraphs come after blank lines.
>
> - Bullet points are okay, too
> - Use a hanging indent
> ```



应该说明代码变动的动机，以及与以前行为的对比。

### 2.3 Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以`revert:`开头，后面跟着被撤销 Commit 的 Header。

> ```
> revert: feat(pencil): add 'graphiteWidth' option
>
> This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
>
> ```

Body部分的格式是固定的，必须写成`This reverts commit <hash>.`，其中的`hash`是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的`Reverts`小标题下面。