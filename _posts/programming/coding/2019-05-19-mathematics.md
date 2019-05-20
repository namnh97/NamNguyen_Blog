---
title: "Mathematic"
categories: [Programming, Algorithm]
toc: true
---

# Primes.
## Normal
```
public boolean isPrime(int n){
    if(n <= 1) return false;
    if(n == 2) return false;
    if(n % 2 == 0) return false;
    int m = Math.sqrt(n);
    for(int i = 3; i <= m; i += 2){
        if(n % i == 0) return false;
    }
    return true;
}
```
## Sieve of Eratosthenes
```
public boolean[] sieve(int n){
    boolean[] prime = new boolean[n + 1];
    Arrays.fill(prime, true);
    prime[0] = false;
    prime[1] = false;
    int m = Math.sqrt(n);
    for(int i = 2; i < m; i++){
        if(primes[i]){
            for(int k = i * i; k <= n; k += i){
                primes[k] = false;
            }
        }
    }
    return primes;
}
```

# GCD

```
public int GCD(int a, int b){
    if(b == 0) return a;
    return GCD(b, a % b);
}
```

# LCM

```
public int LCM(int a, int b){
    return b * a/ GCD(a, b);
}
```

# Base

```
public int toDecimal(int n, int b){
    int result = 0;
    int multiplier = 1;
    while(n > 0){
        result += n % 10*multiplier;
        multiplier = b;
        n = n/10;
    }
    return result;
}
```

## Convert from a decimal number n to a number in base b
```
public int fromDecimal(int n, int b){
    int result = 0;
    int multiplier = 1;
    while(n > 0){
        result += n % b*multiplier;
        mulplier = 10;
        n /= b;
    }
    return result;
}
```

# Fractions and Complex Numbers
## add.
```
public int[] addFractions(int[] a, int[] b){
    int denom = LCM(a[1], b[1]);
    int[] c = {denom/a[1] * a[0] + denom/b[1] * b[0], denom};
    return c;
}
```

## reduce fractions;
```
public void reduceFraction(int[] a){
    int b = GCD(a[0], a[1]);
    a[0] /= b;
    a[1] /= b;
}
```
*src: Topcoder*