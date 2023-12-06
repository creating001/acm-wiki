# 高斯消元

## 高斯消元求解方程组

> 板子题网址: https://www.luogu.com.cn/problem/P3389

```cpp
inline int gauss() {
    int r, c;
    for (r = 0, c = 0; c < n; c++) {
        int t = r;
        for (int i = r; i < n; i++)
            if (fabs(a[i][c]) > fabs(a[t][c])) t = i;
        if (fabs(a[t][c]) < ESP) continue;
        for (int i = c; i < n + 1; i++)
            swap(a[t][i], a[r][i]);
        for (int i = n; i >= c; i--)
            a[r][i] /= a[r][c];
        for (int i = r + 1; i < n; i++)
            for (int j = n; j >= c; j--)
                a[i][j] -= a[i][c] * a[r][j];
        r++;
    }
    if (r < n) {
        for (int i = r; i < n; i++)
            if (fabs(a[i][n]) > ESP) return -1;
        return 1;
    }
    for (int i = n - 1; i >= 0; i--)
        for (int j = i + 1; j < n; j++) {
            a[i][n] -= a[i][j] * a[j][n];
        }
    return 0;
}
```

## 高斯消元解异或方程

> 板子题网址: https://www.acwing.com/problem/content/886

```cpp
inline int gauss() {
    int r, c;
    for (r = 0, c = 0; c < n; c++) {
        int t = r;
        for (int i = t; i < n; i++)
            if (a[i][c] == 1) t = i;
        if (!a[t][c]) continue;
        for (int i = c; i <= n; i++) swap(a[t][i], a[r][i]);
        for (int i = r + 1; i < n; i++)
            if (a[i][c])
                for (int j = c; j <= n; j++)
                    a[i][j] ^= a[r][j];
        r++;
    }
    if (r < n) {
        for (int i = r; i < n; i++)
            if (a[i][n]) return -1;
        return 1;
    }
    for (int i = n - 1; i >= 0; i--)
        for (int j = i + 1; j < n; j++)
            if (a[i][j]) a[i][n] ^= a[j][n];
    return 0;
}
```