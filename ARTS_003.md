# Algorithm

题目：[3sum-closest](https://leetcode.com/problems/3sum-closest/)

难度：medium

思路：最简单最笨的办法就是所有情况都计算一遍,使用三个 for 循环,将所有三个数相加的结果计算出来和 target 比较,使用一个变量始终赋值为最近的那个和.最后返回即可,时间复杂度为 0(n^3)

```js
// version 1 O(n^3)
var threeSumClosest = function(nums, target) {
    let sumClost = nums[0] + nums[1] + nums[2],
        subtract = Math.abs(nums[0] + nums[1] + nums[2] - target)
    for (let i = 0; i < nums.length - 2; i++) {
        for (let j = i + 1; j < nums.length - 1; j++) {
            for (let k = j + 1; k < nums.length; k++) {
                if (Math.abs(nums[i] + nums[j] + nums[k] - target) < subtract) {
                    subtract = Math.abs(nums[i] + nums[j] + nums[k] - target)
                    sumClost = nums[i] + nums[j] + nums[k]
                }
            }
        }
    }
    return sumClost
};
```

还有一种是先对整个数组进行排序(O(nlog(n))),然后使用两个 for 循环就可以找出那个最近的和(O(n^2)).因为整个数组已经排好序了,最外层 for 循环循环第一个数到 length-2.在其中设置两个变量分别为第一个数的索引加一,以及倒数一个数.然后对两个变量循环,判断这三个索引对应的数和 target 的比较,如果小了,那就更小的索引加一,大了就更大的索引减一,同时不断更新记录其中最小的和.直到三个数和 target 相等直接返回或者小索引赶上了大索引,则进入下一个.排好序省下来了很多不需要的比较,比如说当三个数的和小于 target 时,就没必要小索引和更小的大索引相加再和 target 比较.

```js
// version 2 O(n^2)
var threeSumClosest = function(nums, target) {
    let result = nums[0] + nums[1] + nums[nums.length - 1],
        p = 0,
        q = 0,
        sum = 0
    // 从小到大排序
    // O(nlog(n))
    nums.sort((a, b) => a-b)
    //O(n^2)
    for (let i = 0; i < nums.length - 2; i++) {
        p = i + 1
        q = nums.length - 1
        while (p < q) {
            sum = nums[i] + nums[p] + nums[q]
            // 如果直接和 target 一样,那下面的也不用再比较了,这就是最近的,直接返回即可
            if (sum === target) {
                return sum
            }
            // 不断更新最接近 target 的值
            if (Math.abs(sum - target) < Math.abs(result - target))  {
                result = sum
            }
            sum < target ? p++ : q--
        }
    }
    return result
};
```



# Review

文章：[Learning-to-code-by-writing-code-poems](https://medium.com/@smashingmag/learning-to-code-by-writing-code-poems-cd29cd3ba320)

体会：

- 写代码和学习一门语言是很类似的,计算机语言和现实世界交流的语言是很相似的,不要觉得很难,其实很简单而且乐趣无穷
- 写代码要尽可能的符合人的常理,比如说变量名很清晰,函数内容很清晰,注释清晰,让人一眼就能看出来这个变量是用来做什么的,这个函数的功能是什么
- 总而言之就是要写出人性化的代码,通俗易懂,非常优雅撒

# Tip:

## Mac的使用技巧

### Finder

1. 文件夹以tab窗口形式打开，按住command再双击文件夹(前提general最后一个设置了)

2. 常用文件夹可以添加到侧边栏中(我的收藏那里)，直接拖过去就ok.

3. 设置搜索规则，新建智能文件夹，存储右边点击+可以制定规则，然后按住option最右边变为…可以进行详细筛选。诸如设置大文件呀，扩展名为某某的呀等等好好用的。

4. 自定义工具栏，想要那个直接拖到工具栏上即可。还可以拖自己的程序文件夹，按住command拖到工具栏上即可，不要了同样按住command拖走即可，牛逼！

5. 灵活利用tag，可以保存各种类别文件，非常有利于寻找归类文件！！！

6. 重命名多个文件，选中多个文件然后选择重命名这么多个文件.
7. 多桌面灵活切换，可以用于编程和查询文档同时进行，66666.还有hot corners也在mission control中设置，可以设置移动到屏幕四个角触发的动作，牛逼啊

### terminal

1. 查看dns解析：nslookup,输入域名即可。

2. 显示隐藏文件：`defaults write com.apple.finder AppleShowAllFiles -bool true`   ` KillAll Finder`
3. 隐藏文件把true改为false即可

# Share

文章：[js中浅拷贝和深拷贝的区别](https://blog.csdn.net/m0_37679293/article/details/87987211)

