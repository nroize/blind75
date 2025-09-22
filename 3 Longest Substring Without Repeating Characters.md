# 3. Longest Substring Without Repeating Characters
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/?envType=problem-list-v2&envId=oizxjoit

## Code
```cpp
int lengthOfLongestSubstring(string s) {
    if ( s.size() == 1 ) return 1;
    std::unordered_map<char, int> lastSeenIdx;
    
    int left = 0;
    int longestRun = 0;

    for ( int right = 0; right < s.size(); right++ )
    {
        char current = s[ right ];

        if ( lastSeenIdx.find( current ) != lastSeenIdx.end() && lastSeenIdx[ current ] >= left )
        {
            left = lastSeenIdx[ current ] + 1;
        }

        lastSeenIdx[ current ] = right;
        longestRun = std::max( longestRun, right - left + 1 );
    }

    return longestRun;
}
```

## Basic idea
Maintain a map of the index at which we last saw any given character. Create a sliding window and progressively expand it to the right – if we see a character that's within the sliding window, move the left side over and update the position of that character in the map to this new one, otherwise continue. Update the length of the run based on the size of the window, largest window = longest sequence.

## Time complexity
Assuming $O(1)$ lookup for `unordered_map`, we iterate over the array just once and thus have $O(n)$ complexity.