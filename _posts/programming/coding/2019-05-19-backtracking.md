---
title: "Backtracking"
categories: [Programming, Algorithm]
---

```
vector permutation(N);
vector used(N, 0);

void try(int which, int what) { 
    permutation[which] = what;
    used[what] = 1;
    if (which == N - 1) { 
        outputPermutation();
    } else { 
        for (int next = 0; next < N; next++) { 
            if (!used[next]) { 
                try(which + 1, next);
            }
            used[what] = 0;
        }
    }
}

int main() { 
    for (int first = 0; first <= N; first++) {
        try(0, first);
    }
}
```