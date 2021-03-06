## 1. LeetCode 136 [Single Number](https://leetcode.com/problems/single-number/)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int size = nums.size();
        int result = 0;
        for(int i=0; i<size; i++) {
            result = result xor nums[i];
        }
        return result;
    }
};
```



## 2. LeetCode 137 [Single Number II](https://leetcode.com/problems/single-number-ii/)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int size = nums.size();
        int a = 0, b = 0;
        for(int i=0; i<size; i++) {
            a = (a ^ nums[i]) & ~b;
            b = (b ^ nums[i]) & ~a;
        }
        return a;
    }
};
```



## 3. LeetCode 260 [Single Number III](https://leetcode.com/problems/single-number-iii/)

```c++
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int size = nums.size();
        int a = 0;
        for(int i=0; i<size; i++) {
            a = a ^ nums[i];
        }
        // cout << a << endl;
        a &= (-a);
        // cout << a << endl;
        vector<int> result = {0, 0};
        for(int i=0; i<size; i++) {
            if((nums[i] & a) == 0) {
                result[0] ^= nums[i];
            } else {
                result[1] ^= nums[i];
            }
        }
        return result;
    }
};
```



## 4. LeetCode 191 [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int cnt = 0;
        for(int i=0; i<32; i++) {
            if(n & 1) cnt++;
            n >>= 1;
        }
        return cnt;
    }
};
```



## 5. LeetCode 78 [Subsets](https://leetcode.com/problems/subsets/)

```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int n = (int)nums.size();
        int m = (int)pow(2,n);
        vector<vector<int>> subs(m, vector<int>());
        for(int i=0,q=1; i<n; i++,q<<=1) {
            for(int j=q; j<m; j+=q) {
                for(int k=0; k<q; k++) {
                    subs[j++].push_back(nums[i]);
                }
            }
        }
        return subs;
    }
};
```



## 6. LeetCode 190 [Reverse Bits](https://leetcode.com/problems/reverse-bits/)

```c++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        n = (n >> 16) | (n << 16);
        n = ((n & 0xff00ff00) >> 8) | ((n & 0x00ff00ff) << 8);
        n = ((n & 0xf0f0f0f0) >> 4) | ((n & 0x0f0f0f0f) << 4);
        n = ((n & 0xcccccccc) >> 2) | ((n & 0x33333333) << 2);
        n = ((n & 0xaaaaaaaa) >> 1) | ((n & 0x55555555) << 1);
        return n;
    }
};
```



## 7. LeetCode 338 [Counting Bits](https://leetcode.com/problems/counting-bits/)

```c++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> dp(num+1, 0);
        int offset = 1;
        for (int i=1; i<=num; i++) {
            if (i == offset * 2) {
                offset *= 2;
            }
            dp[i] = dp[i-offset] + 1;
        }
        return dp;
    }
};
```



## 8. LeetCode 401 [Binary Watch](https://leetcode.com/problems/binary-watch/)

```c++
class Solution {
public:
    vector<string> readBinaryWatch(int num) {
        vector<string> result;
        for(int h = 0; h < 12; h++) {
            for(int m = 0; m < 60; m++) {
                if(bitset<10>(h << 6 | m).count() == num) {
                    result.emplace_back(to_string(h) + (m < 10 ? ":0" : ":") + to_string(m));
                }
            }
        } 
        return result;
    }
};
```



## 9. LeetCode 461 [Hamming Distance](https://leetcode.com/problems/hamming-distance/)

```c++
// solution 1
class Solution {
public:
    int hammingDistance(int x, int y) {
        int cnt = 0;
        while(x > 0 || y > 0) {
            (x & 1) != (y & 1) ? cnt++ : 0;
            x >>= 1;
            y >>= 1;
        }
        return cnt;
    }
};

// solution 2
class Solution {
public:
    int hammingDistance(int x, int y) {
        int cnt = 0;
        int z = x ^ y;
        while(z > 0) {
            (z & 1) ? cnt++ : 0;
            z >>= 1;
        }
        return cnt;
    }
};
```



## 10. LeetCode 477 [Total Hamming Distance](https://leetcode.com/problems/total-hamming-distance/)

```c++
class Solution {
public:
    int hammingDistance(int x, int y) {
        int cnt = 0;
        int z = x ^ y;
        while(z > 0) {
            (z & 1) ? cnt++ : 0;
            z >>= 1;
        }
        return cnt;
        /*
        while(x > 0 || y > 0) {
            (x & 1) != (y & 1) ? cnt++ : 0;
            x >>= 1;
            y >>= 1;
        }
        return cnt;*/
    }
};
```



## 11. LeetCode 693 [Binary Number with Alternating Bits](https://leetcode.com/problems/binary-number-with-alternating-bits/)

```c++
class Solution {
public:
    bool hasAlternatingBits(int n) {
        vector<int> v;
        while(n) {
            v.push_back(n % 2);
            n >>= 1;
        }
        for(int i=0; i<v.size()-1; i++) {
            if(v[i] == v[i+1]) return false;
        }
        return true;
    }
};
```



## 12. LeetCode 201 [Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

```c++
class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
        return (n > m) ? (rangeBitwiseAnd(m/2, n/2) << 1) : m;
    }
};
```











































