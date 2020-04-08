---
title: Knapsack Problem
tags: Dynamic Programming
notebook: Leetcode
---
Given the weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. In other words, given two integer arrays val[0..n-1] and wt[0..n-1] which represent values and weights associated with n items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of val[] such that sum of the weights of this subset is smaller than or equal to W. We cannot break an item, either pick the complete item or don’t pick it (0-1 property).

Here W <= 2000000 and n <= 500

Examples:
```
Input : W = 10, n = 3
        val[] = {7, 8, 4}
        wt[] = {3, 8, 6}
Output: 11
We get maximum value by picking items of 3 KG and 6 KG.
```
```c++
#include <iostream>
#include <vector>
using namespace std;
int Knapsack(vector<int> &values, vector<int> &weights, int W);
int main()
{
    vector<int> values = {60, 100, 120};
    vector<int> weights = {10, 20, 30};
    int W = 50;
    cout << Knapsack(values, weights, W) << endl;
    return 0;
}

int Knapsack(vector<int> &values, vector<int> &weights, int W) {
    vector<int> dp(W + 1, 0);
    
    for (int i = 0; i < values.size(); i++) {
        vector<int> tmpDP(dp);
        for (int w = W; w >= weights[i]; w--) {
            tmpDP[w] = max(tmpDP[w], dp[w - weights[i]] + values[i]);
        }
        dp.swap(tmpDP);
    }
    return dp[W];
}
```