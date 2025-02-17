# 分数背包问题

分数背包是 0-1 背包问题的一个变种问题。

!!! question

    给定 $n$ 个物品，第 $i$ 个物品的重量为 $wgt[i-1]$ 、价值为 $val[i-1]$ ，现在有个容量为 $cap$ 的背包，每个物品只能选择一次，**但可以选择物品的一部分，价值根据选择的重量比例计算**，问在不超过背包容量下背包中物品的最大价值。

![分数背包问题的示例数据](fractional_knapsack_problem.assets/fractional_knapsack_example.png)

**第一步：问题分析**

本题和 0-1 背包整体上非常相似，状态包含当前物品 $i$ 和容量 $c$ ，目标是求不超过背包容量下的最大价值。

不同点在于，本题允许只选择物品的一部分，我们可以对物品任意地进行切分，并按照重量比例来计算物品价值，因此有：

1. 对于物品 $i$ ，它在单位重量下的价值为 $val[i-1] / wgt[i-1]$ ，简称为单位价值；
2. 假设放入一部分物品 $i$ ，重量为 $w$ ，则背包增加的价值为 $w \times val[i-1] / wgt[i-1]$ ；

![物品在单位重量下的价值](fractional_knapsack_problem.assets/fractional_knapsack_unit_value.png)

**第二步：贪心策略确定**

最大化背包内物品总价值，**本质上是要最大化单位重量下的物品价值**。由此便可推出本题的贪心策略：

1. 将物品按照单位价值从高到低进行排序。
2. 遍历所有物品，**每轮贪心地选择单位价值最高的物品**。
3. 若剩余背包容量不足，则使用当前物品的一部分填满背包即可。

![分数背包的贪心策略](fractional_knapsack_problem.assets/fractional_knapsack_greedy_strategy.png)

**第三步：正确性证明**

采用反证法。假设物品 $x$ 是单位价值最高的物品，使用某算法求得最大价值为 $res$ ，但该解中不包含物品 $x$ 。

现在从背包中拿出单位重量的任意物品，并替换为单位重量的物品 $x$ 。由于物品 $x$ 的单位价值最高，因此替换后的总价值一定大于 $res$ 。**这与 $res$ 是最优解矛盾，说明最优解中必须包含物品 $x$ 。**

对于该解中的其他物品，我们也可以构建出上述矛盾。总而言之，**单位价值更大的物品总是更优选择**，这说明贪心策略是有效的。

**实现代码**

我们构建了一个物品类 `Item` ，以便将物品按照单位价值进行排序。在循环贪心选择中，分为放入整个物品或放入部分物品两种情况。当背包已满时，则跳出循环并返回解。

=== "Java"

    ```java title="fractional_knapsack.java"
    [class]{Item}-[func]{}

    [class]{fractional_knapsack}-[func]{fractionalKnapsack}
    ```

=== "C++"

    ```cpp title="fractional_knapsack.cpp"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "Python"

    ```python title="fractional_knapsack.py"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractional_knapsack}
    ```

=== "Go"

    ```go title="fractional_knapsack.go"
    [class]{}-[func]{II}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "JavaScript"

    ```javascript title="fractional_knapsack.js"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "TypeScript"

    ```typescript title="fractional_knapsack.ts"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "C"

    ```c title="fractional_knapsack.c"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "C#"

    ```csharp title="fractional_knapsack.cs"
    [class]{Item}-[func]{}

    [class]{fractional_knapsack}-[func]{fractionalKnapsack}
    ```

=== "Swift"

    ```swift title="fractional_knapsack.swift"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "Zig"

    ```zig title="fractional_knapsack.zig"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

=== "Dart"

    ```dart title="fractional_knapsack.dart"
    [class]{Item}-[func]{}

    [class]{}-[func]{fractionalKnapsack}
    ```

如下图所示，如果将一个 2D 图表的横轴和纵轴分别看作物品重量和物品单位价值，则分数背包问题可被转化为“求在有限横轴区间下的最大围成面积”。这个类比可以帮助我们从几何角度清晰地看到贪心策略的有效性。

![分数背包问题的几何表示](fractional_knapsack_problem.assets/fractional_knapsack_area_chart.png)

最差情况下，需要遍历整个物品列表，**因此时间复杂度为 $O(n)$** ，其中 $n$ 为物品数量。由于初始化了一个 `Item` 对象列表，**因此空间复杂度为 $O(n)$** 。
