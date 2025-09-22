# 1. Two Sum
https://leetcode.com/problems/two-sum/submissions/1776327335/?envType=problem-list-v2&envId=oizxjoit

## Code
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    std::unordered_map<int, int> numMap;

    for ( int i = 0; i < nums.size(); i++ )
    {
        int complement = target - nums[ i ];

        if ( numMap.find( complement ) != numMap.end() )
        {
            return { i, numMap[ complement ] };
        }

        numMap[ nums[ i ] ] = i;
    }

    return { -1, -1 };
}
```

## Basic idea
Keep track of the index of each value in an `unordered_map`. For each new number, check if its complement exists in the map. If it does, return the index for the complement from the map and the index of the current value. If not, insert the current value and its index and continue.

## Time complexity
Assuming `unordered_map` has $O(1)$ lookup, each value will only be visited once at most. Therefore, $O(n)$ time complexity.