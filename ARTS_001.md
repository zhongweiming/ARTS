# Algorithm

题目：[two-sum](https://leetcode.com/problems/two-sum/)

难度：easy

思路：这道题的一般思路是第一个开始和第二个到最后一个相加看看会不会等于目标，不行从第二个开始，到代码中就是两个for循环

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0;i < nums.length-1;i++){
            for(int j = i+1;j < nums.length;j++){
                if(nums[i]+nums[j]==target)
                    return new int[]{i,j};
            }
        }
        return null;
    }
}
```

这样做的话时间复杂度为O(n^2),空间复杂度为O(1)

第二种是用java的HashMap

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length;i++){
            int content = target - nums[i];
            if(map.containsKey(content)){
                return new int[] { map.get(content), i };
            }
            map.put(nums[i],i);
        }
        throw new IllegalArgumentException("Cannot find the solution");
    }
}
```
此时的时间复杂度为O(n),空间复杂度也是O(n)

# Review

文章：[How to think like a programmer](https://medium.freecodecamp.org/how-to-think-like-a-programmer-lessons-in-problem-solving-d1d8bf1de7d2)

体会：
- 编程就是用一种更加高效的思维去学会更加高效的解决一个问题
- 解决问题是核心，专注于语法而不是问题解决是一个很大的错误！
- 如何解决一个问题：
  - 两步:
  - 1.解决问题的一个框架流程
  - 2.不断地训练
  - 解决问题的流程:
  - 首先要理解这个问题，很清晰的说出这个问题是什么
  - 然后要有一个解决问题的计划，我该怎么来解决这个问题(给出一个输入x,通过哪些步骤可以得到结果y)
  - 把问题划分成一个个小问题，从最简单的开始解决，自己知道怎么解决的问题开始，最后connect dots。就像一个算法题哈，要学会分解问题。比如求一堆数中第三大的数怎么求，如果难的话，那么求三个数中第三大的数？如此将问题一步步简单化到你能解决的程度，再慢慢的增加难度不断解决！
  - 如果卡住了
    - debug，debug的艺术不是搞清楚你认为你的程序该怎么执行而是搞清楚你的程序现在是怎么执行的，这才能找到bug，如果一直以自己认为的那样去debug则一直觉得没错。
    - 退回一步再看这个问题，看看是否还有其它的办法，或者直接重新开始另一种思路
    - 借助搜索引擎，你遇到的问题可能别人也曾经遇到过，搜索小问题的解决办法，而不是大问题，要能够从中学习到什么，否则就是浪费时间。对于比较妙难的问题，自己解决了之后也可以去搜索看看别人是怎么解决的。
  - 最后就是不断地按照这种方式找问题，去解决一个个问题，比如可以玩能够将问题分解并且解决的游戏呀，做编程题呀等等哇哇！爱上解决问题，这才能真正成为一个优秀的软件工程师！


# Tip:

常用的sublime快捷键/插件：

1. 左右文件切换fn+ctrl+up or down

2. 无论光标在哪里，换行：command+enter

3. 用浏览器打开：ctrl+alt+v

4. 搜索：command+shift+p

5. 复制本行到下一行:command+shift+d

6. 代码自动对齐:ctrl+q

7. 删除整行：ctrl+shift+k

8. 查找替换所有相同内容:command+shift+f

9. 安装新插件（非常好用，可以支持各种语言包啥的）：

command+shift+p,输入pcip再输入想要的插件,ojbk

10. 要在多行同一个位置修改相同的东西，按住alt,下拉

11. 神插件emmet，能想到的都有，牛逼，参考

12. 在当前文件所在目录打开终端：

command+shift+t

13. 选中长度不一的一列单词，ctrl+shift+左右键

14. 选中所有相同的，先选择一个，再按command+d，要继续一直按d

15. 选中所有相同的，先选择一个，再按command+ctrl+G



# Share

文章：[js正则表达式](https://blog.csdn.net/m0_37679293/article/details/82931152)




