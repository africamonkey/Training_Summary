# 2017-2018 ACM-ICPC Pacific Northwest Regional Contest (Div. 1)

Date: 2018-03-01

## Practice Link

https://vjudge.net/contest/214250

## 个人总结

### 王凯祺

前期刷水题我们的节奏都很不错。这套题有非常非常多的水题。

做完水题后剩下BHKM四道题。B题黄镇搞了个 12! 的暴力，TLE。

我搞H题，怎么试样例怎么对，交上去发现WA4。我第一反应是斜率优化的时候 k1 * b2 >= k2 * b1 时爆 long long 了，无奈 Codeforces 没有 int128 。
赛后改成 (long double)k1 / k2 >= (long double)b1 / b2 过了……
然后一直在琢磨，k <= 2 * 10^6, b <= 10^12 ，怎么可能爆 long long 。

结果发现我加线段的时候竟然加了 b = inf 的线段进来。

太粗心了！

## 题解

### H题

把航班拆成两个事件，起飞和降落，然后按照时间排序。

起飞时，在起飞城市查询哪个到达时间转移过来最棒。

这里用凸包来优化，每个城市建一个凸包。

设当前时刻为 x ，f[x]表示时刻x的答案。

f[x] = f[y] + x^2 - 2xy + y^2

其中 y 为到达该城市的时刻。

我们可以令 k = -2y, b = y^2 + f[y] ，将到达时刻插入该城市的凸包。

到达时，直接转移啊。
