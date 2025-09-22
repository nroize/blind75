# 647. Palindromic Substrings
https://leetcode.com/problems/palindromic-substrings/?envType=problem-list-v2&envId=oizxjoit

## Code
```cpp
int countSubstrings(string s) {
    if ( s.size() == 1 )
    {
        return 1;
    }

    int count = 0;

    for ( int i = 0; i < s.size(); i++ )
    {
        expand( i, i, count, s ); // odd
        expand( i, i + 1, count, s ); // even
    }

    return count;
}

void expand( int left, int right, int& count, std::string& s )
{
    while ( left >= 0 && right < s.size() && s[ left ] == s[ right ])
    {
        left--;
        right++;
        count++;
    }
}
```

## Basic idea
Similar logic to `5 Longest Palindrome String`. Keep a count of the lengths of valid palindromes from each point (even and odd), return that length.

## Time complexity
In the worst case, we end up iterating loop in `expand` across the entire string for each character (e.g. in the string "aaaaa"), so our time complexity becomes $O(n^2)$.