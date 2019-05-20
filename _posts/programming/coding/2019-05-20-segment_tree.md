---
title: "Segment Tree"
categories: [Programming, Algorihtm]
---

# Classic Segment Tree(\\(log_2 n\\))
```
//problem: https://codeforces.com/contest/380/problem/C

void build(int id = 1, int l = 0, int r = n) {
    if (r - l < 2) {
        if (s[l] == '(') {
            o[id] = 1;
        } else { 
            c[id] = 1;
        }
        return;
    }
    int mid = (l + r) / 2;
    build(2 * id, l, mid);
    build(2 * id + 1, mid, r);
    int tmp = min(o[2 * id], c[2 * id + 1]);
    t[id] = t[2 * id] + t[2 * id + 1] + tmp;
    o[id] = o[2 * id] + o[2 * id + 1] - tmp;
    c[id] = c[2 * id] + c[2 * id + 1] - tmp;
}

typedef pair<int, int> pii;
typedef pair<int, pii> node;
node segment(int x, int y, int id = 1, int l = 0,int r = n) {
    if (l >= y || x >= r)  return node(0, pii(0, 0));
    if (x <= l && r <= y) {
        return node(t[id], pii(o[id], c[id]));
    }
    int mid = (l + r) / 2;
	node a = segment(x, y, 2 * id, l , mid);
	node b = segment(x, y, 2 * id + 1, mid, r);
	int T, temp, O, C;
	temp = min(a.y.x, b.y.y);
	T = a.x + b.x + temp;
	O = a.y.x + b.y.x - temp;
	C = a.y.y + b.y.y - temp;
	
	return node(T, pii(O, C));
}


```

*src: codeforces.com*
