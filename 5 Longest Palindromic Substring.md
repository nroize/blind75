# 5. Longest Palindromic Substring
https://leetcode.com/problems/longest-palindromic-substring/?envType=problem-list-v2&envId=oizxjoit

## Code
```cpp
string longestPalindrome(string s) {
    if ( s.size() == 0 ) return "";

    int start = 0;
    int end = 0;

    for ( int i = 0; i < s.size(); i++ )
    {
        int odd = expand( s, i, i ); // longest palindrome if centered around character i (odd-length palindrome)
        int even = expand( s, i, i + 1 ); // longest palindrome if centered around chars i and i + 1 (even-length palindrome)

        int max_len = std::max( odd, even );

        if ( max_len > end - start )
        {
            start = i - ( max_len - 1 ) / 2; // start is 
            end = i + max_len / 2;
        }
    }

    return s.substr( start, end - start + 1 ); // substr accepts starting position and length
}

int expand( const std::string& s, int left, int right )
{
    int n = s.size();
    while ( left >= 0 && right < n && s[ left ] == s[ right ] )
    {
        left--;
        right++;
    }

    return (right - left - 1);
}
```

## Basic idea
Iterate over the characters in the string, checking if there is a longer palindrome centered around that character in an even or odd configuration (i.e. centered around the character `i` or character `i` and `i + 1` respectively)

`expand` will go outwards from the left and right positions past through until the palindrome condition is invalidated, and return the length of the palindrome centered around the provided indices.

## Time complexity
In the worst case, like a string with all the same letter, the outer loop will check every character and the expand method will again check every character, giving us a worst-case time complexity of $O(n^2)$.