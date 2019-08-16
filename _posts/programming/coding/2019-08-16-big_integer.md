
---
title: "Big Interger"
categories: [Programming, Algorithm]
---

```
//https://vn.spoj.com/problems/CHUOIHAT/
#include<bits/stdc++.h>
#define ll long long 
#define FOR(i, a, b) for (int i = (a), _##i = (b); i <= _##i; ++i)
#define FORD(i, a, b) for (int i = (a), _##i = (b); i >= _##i; --i)
#define DEBUG(X) { auto _X = (X); cerr << "L" << __LINE__ << ": " << #X << " = " << (_X) << endl; };

using namespace std;

const int MAX_DIGIT = 30, LOG_BASE = 9, BASE = 1000000000;
const int N = 250 + 5;
struct BigInteger {
	int d[MAX_DIGIT], n;
	void operator = (const int &x) { 
		memset(d, 0, sizeof(d)); n = 0;
		for (int t = x; t != 0; t /= BASE) {
			d[n++] = t % BASE;
		}
	}


	bool operator < (const BigInteger &a) const { 
		if (n < a.n) return true;
		if (n > a.n) return false;
		for (int i = n - 1; i >= 0; i--) {
			if (d[i] < a.d[i]) return true;
			else if(d[i] > a.d[i]) return false;
		}
		return false;
	}


	void operator += (const BigInteger &a) {
		int rem = 0; n = max(n, a.n);
		for (int i = 0; i < n; i++) {
			int p = d[i] + a.d[i] + rem;
			if (p >= BASE) d[i] = p - BASE, rem = 1;
			else d[i] = p, rem = 0;
		}
		if (rem) d[n++] = rem;
	}


	void operator -= (const BigInteger &a) {
		int rem = 0;
		for (int i = 0; i <  n; i++) {
			int p = d[i] - a.d[i] - rem;
			if (p < 0) d[i] = p + BASE, rem = 1;
			else d[i] = p, rem = 0;
		}
		while (n > 0 &&  d[n - 1] == 0) --n;
	}
	void scan() { 
		string s; cin >> s; int l = s.size(); 
		reverse(s.begin(), s.end());
		memset(d, 0, sizeof(d));
		for (n = 0; LOG_BASE * n < l; n++) {
			for (int j = min(LOG_BASE * (n + 1), l) - 1; j >= LOG_BASE * n; j--) {
				d[n] = d[n] * 10 + s[j] - '0';
			}
		}
	}
}f[N][2 * N];

int main(void){
	int n; BigInteger x;
	cin >> n; x.scan();
	for (int v = 2 * n; v >= n; v--) f[n][v] = 1;
	for (int p = n - 1; p >= 1; --p) {
		for (int v = 2 * p; v >= p; v--) { 
			for (int nv = 2 * (p + 1); nv > v; --nv){
				f[p][v] += f[p + 1][nv];
			}
		}
	}
	for (int p = 1, v = 1; p <= n; ++p, ++v){
		while(f[p][v] < x) x -= f[p][v], v++;
		if(p > 1) cout << " ";
		cout << v;
	}
	return 0;
}

```
*reference: happyboy99x*