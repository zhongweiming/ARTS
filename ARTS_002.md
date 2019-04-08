# Algorithm

题目：[reverse-integer](https://leetcode.com/problems/reverse-integer/)

难度：easy

思路：这道题有两种思路,一种是数字方法,一种是字符串方法

数字方法:首先将所有数字提取出来,然后通过乘 10 加数的方法实现

一开始用了数组,很多变量,后面发现内存占用大,速度也更慢,后面慢慢改进,直到最后,速度超过 99%,内存占用超过 80%多,内存实在是极限了,不知道是不是 leetcode 运行的问题

```java
/**
 * @param {number} x
 * @return {number}
 */
// version 1
// var reverse = function(x) {
//     let result = 0,
//         arr = []
//     while (Math.abs(x) !== 0) {
//         arr.push(x % 10)
//         x = parseInt(x / 10)
//     }
//     for (let i = 0; i < arr.length; i++) {
//         result = result * 10 + arr[i]
//     }
//     if (Math.abs(result) >= Math.pow(2, 31)) {
//         return 0
//     }
//     return result
// };
    //version 2 减少变量,降低内存占用
// var reverse = function (x) {
//         let result = 0
//         while (Math.abs(x) !== 0) {
//             result = result * 10 + x % 10
//             x = parseInt(x / 10)
//         }
//         if (Math.abs(result) >= Math.pow(2, 31)) {
//             return 0
//         }
//         return result
//     };
    // version 3 减少计算,提高速度
var reverse = function (x) {
    let result = 0
    while (x !== 0) {
        result = result * 10 + x % 10
        x = parseInt(x / 10)
    }
    if (result > 0x7FFFFFFF || result < -0x80000000) {
        return 0
    }
    return result
};

// version 4 减少语句
var reverse = function(x) {
    let result = 0
    while (x !== 0) {
        result = result * 10 + x % 10
        x = parseInt(x / 10)
    }
    return (result > 0x7FFFFFFF || result < -0x80000000) ? 0 : result
};
```

第二种利用字符串:将数转换成字符串然后转成字符数组,转置,再转成字符串,再转成整数,后面用了一个 ES6 中的一个 Math 方法(Math.sign),获取数的符号,乘以前面的整数就是最后的结果

本来以为可能会更快,然而并没有,还更慢了,可能执行的方法多,内存也没有改善.

```java
// version 5 字符串方法 额,好像还更慢且内存也没有节省
var reverse = function(x) {
    let result = 			parseInt(Math.abs(x).toString().split('').reverse().join('')) * Math.sign(x)
    return (result > 0x7FFFFFFF || result < -0x80000000) ? 0 : result
}
```

# Review

文章：[How JavaScript works: an overview of the engine, the runtime, and the call stack](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf)

体会：

- V8 引擎包括两个主要的组件

  - Memory Heap--内存分配发生的地方
  - Call Stack--程序代码执行的地方

- Call Stack 是一个记录了程序执行的地方的数据结构,入栈出栈的方式执行代码块

- 异常的追踪会从最开始抛出异常的函数开始,一直追踪到执行的最开始的函数,显示该函数的位置,如:

- ```js
  function foo() {
      throw new Error('SessionStack will help you resolve 				crashes :)');
  }
  function bar() {
      foo();
  }
  function start() {
      bar();
  }
  start();
  ```

- ![](/Users/zhongweiming/Downloads/%E5%BC%82%E5%B8%B8.png)

- "**Blowing the stack**"发生在已经达到栈的最大size 之时.如下

- ```js
  function fun() {
      fun()
  }
  fun() // RangeError: Maximum call stack size exceeded
  ```

- 单线程很简单,没有复杂的并发问题需要处理,但是如果某个任务执行需要很长的时间,则会导致浏览器停止不动,严重影响用户体验,这个时候就需要用到 js 的异步编程了

# Tip:

## Git

### git 命令

1. 创建新本地仓库：git init +repo_name

2. 创建裸仓库：git init --bare+repo_name

3. 克隆仓库：git clone 要克隆的仓库路径  克隆后的仓库路径

4. 对克隆的仓库修改提交完后，直接git push就可以上传到gitee或者github上

5. 将工作区文件添加到暂存区：git add 文件路径

6. 添加到历史区：git commit –m “日志信息”

7. 查看git状态：git status（修改工作区文件时会有提示）

8. 查看工作区和历史区不同:git diff xxx文件

9. git log --oneline可以查看简单的提交信息，包括commit-id和记录。

10. 删除暂存区和工作区文件:git rm

11. 替换移动(相当于重命名)工作区文件 git mv(此操作会重命名工作区和暂存区文件，如果暂存区里面的文件删除了则不能重命名,版本问题貌似)

12. 忽略不想添加到暂存区的文件：gitignore。在工作目录下创建.gitignore文件，将需要忽略的文件写在里面。并且可以将其添加到版本库中，用于整个仓库的共享。

*.[oa](以.o .a结尾的忽略)

*~(以~结尾的忽略)

!test.pyc(原来忽略，现在想纳入进来)

/!test.py(同上，本身有感叹号)

res/(忽略目录)

**/res(忽略所有res目录)

13. 还原删除的文件：git reset HEAD 文件名。再加上git checkout 文件名，可以还原到工作区。

14. 删除暂存区和版本区的文件：git rm --cache +文件名

15. 添加所有文件到暂存区：git add .或者git add -A

16. 与远程仓库建立联系：

git remote add origin [git@github.com:用户名/repo.git](mailto:git@github.com:用户名/repo.git)

17. 上传到远程仓库：

git push -u origin master.之后的上传可以省略u

18. 创建新分支：git branch branch_name

19. 切换分支：git checkout branch_name

20. 创建并切换分支：git checkout -b branch_name

21. 合并分支(主分支上)：git merge branch_name(其它分支)

22. 删除分支：git branch -d branch_name

23. 查看分支合并图：详细：git log --graph 简单：git log --graph --oneline

24. 强制不使用fast-forward方法，git merge --no-ff -m "merge with no-ff" branch2

25. HEAD指向当前版本，要在版本之间穿梭，使用git reset --hard commit-id(HEAD^表示上一个版本，往上多个版本可以使用HEAD~num),如果回退之后想要回来，找不到后面的commit-id，可以用git reflog查看命令历史，以便找到对应commit-id.

26. git checkout -- filename,如果修改后没有add,回到版本库最新状态，已经add 过了，修改了工作区，则回到暂存区状态。Add到暂存区想撤销，使用git reset HEAD filename,然后用上面命令退回去。

27. rm filename删除文件，如果想要恢复，可以git checkout -- filename,从版本库恢复。要彻底删除文件包括版本库，git rm filename, git commit -m “”。

28. 强行删除一个未合并过的分支,

git branch -D branch_name

29. 创建标签git tag <tagname> commit_id(不写默认最新提交)，指定标签信息：git tag  -a <tagname> -m “xxx” commit_id,查看所有标签：git tag,查看某个标签详情：git show <tagname>

30. 命令git push origin <tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除一个本地标签；

命令git push origin :refs/tags/<tagname>可以删除一个远程标签



# Share

文章：[总结js中apply,call和bind的区别](<https://blog.csdn.net/m0_37679293/article/details/87949437>)

