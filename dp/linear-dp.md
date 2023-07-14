# 线性DP

## 最长上升子序列

> 板子题网址: https://www.acwing.com/problem/content/898

给定一个长度为 $n$ 的序列 $a$，求它的最长上升子序列的长度。

```cpp
//时间复杂度O(n^2)
inline int LIS(int* a, int n) {
    for (int i = 0; i < n; i++) dp[i] = 1;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < i; j++)
            if (a[i] > a[j])
                dp[i] = max(dp[i], dp[j] + 1);
    return *max_element(dp, dp + n);
}
```

```cpp
//时间复杂度O(nlogn)
inline int LIS(int* a, int n) {
    int len = 1;
    dp[1] = a[0];
    for (int i = 1; i < n; i++)
        if (a[i] > dp[len])
            dp[++len] = a[i];
        else {
            int pos = lower_bound(dp + 1, dp + len + 1, a[i]) - dp;
            dp[pos] = a[i];
        }
    return len;
}
```

## 最长公共子序列

> 板子题网址: https://www.acwing.com/problem/content/899

```cpp
inline int LCS(int* a, int* b, int n, int m) {
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            if (a[i] == b[j])
                dp[i][j] = dp[i - 1][j - 1] + 1;
            else
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
    return dp[n][m];
}
```

## 编辑距离

```cpp
inline int edit_distance(string& a, string& b) {
    int n = a.size(), m = b.size();
    for (int i = 0; i <= n; i++) dp[i][0] = i;
    for (int i = 0; i <= m; i++) dp[0][i] = i;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= m; j++)
            if (a[i - 1] == b[j - 1])
                dp[i][j] = dp[i - 1][j - 1];
            else
                dp[i][j] = min({dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]}) + 1;
    return dp[n][m];
}
```