---
title: "String Manipulate"
categories: [Programming, Algorithm]
---

# Split string
```
vector<string> split(const string &s, char delimiter) {
    vector<string> tokens;
    string token;
    isstringstream tokenStream(s);
    while (getline(tokenStream, token, delimiter)) {
        tokens.push_back(token);
    }
    return tokens;
}
```