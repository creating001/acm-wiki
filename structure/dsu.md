# 并查集

> 板子题网址: https://www.luogu.com.cn/problem/P3367

## 数据结构

```cpp
// N 为最大点数, p[i] 表示 i 的父节点, size[i] 表示 i 所在集合的大小
int p[N], size[N];
```

## 初始化

```cpp
inline void init() {
    for (int i = 0; i < N; i++) p[i] = i, siz[i] = 1;
}
```

## 查找

```cpp
inline int find(int x) {
    return (p[x] == x ? x : p[x] = find(p[x]));
}
```

## 合并

```cpp
inline void unite(int x, int y) {
    int px = find(x), py = find(y);
    if (find(x) == find(y)) return;
    siz[py] += siz[px], p[px] = py;
}
```

## 判断是否连通

```cpp
inline bool is_connect(int x, int y) {
    return find(x) == find(y);
}
```