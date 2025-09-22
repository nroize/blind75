# 128. Longest Consecutive Sequence

https://leetcode.com/problems/longest-consecutive-sequence/description/?envType=problem-list-v2&envId=oizxjoit

## Code
```cpp
int longestConsecutive(vector<int>& nums) {
    std::unordered_set<int> numsSet( nums.begin(), nums.end() );

    int longestRun = 0;

    for ( int num : numsSet )
    {
        if ( numsSet.find( num - 1 ) == numsSet.end() ) // smallest value in a run
        {
            int runLength = 1;
            while ( numsSet.find( num + runLength ) != numsSet.end() ) runLength++; // go to end of run
            longestRun = std::max( longestRun, runLength );
        }
    }

    return longestRun;
}
```

## Basic idea
Convert vector into a set, iterate over set searching for the first value in each consecutive run (i.e. the number one lower than it isn't in the set), then iterate until you reach the end of a run.

## Time complexity
* Building the set: $O(n)$
* Outer loop: $O(n)$ iterations, doing $O(1)$ work + the possibility of entering the inner loop
* Inner loop: $O(n)$ iterations, accessing each element exactly once

Since the inner loop only visits each set element at most once, and will only run for values that start a consecutive sequence, the overall time complexity is $O(n)$.