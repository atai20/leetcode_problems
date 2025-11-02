Problem:
![Alt text](Palindrome%20problem.png)

my attempt:


stupid solution \/
General plan is to first count how many digits we have = n, then make a cycle for n/2 steps that goes from 0 to n/2 and the other one of parallel goes from n-1 to n/2+1 comparing them



``` C++
class Solution {
public:
    bool isPalindrome(int x) {
        if(x<0){
            return false;
        }else{
            int digits = 1;
            int original = x;
            while(x/10!=0){
                digits++;
                x = x/10;
            }
            for (int i =0; i<digits/2; i++){

                original = original-(digits-1)*(x%10);

            }
            if(original == 0){
                return true;
            }else{
                if(digits%2==0){
                    return false;
                }else{
                    return true;
                }
            }

        }
    }
};

```



better use the stack logic here, first add all the digits to array(or vector in this case since you don't know the length) and then check if it is equal to the one after you did the swap:

new attempt code, didn't check compilation yet:

``` C++
#include <vector>

class Solution {
public:
    bool isPalindrome(int x) {
        std::vector<int> digits;
        int y = x;
        if(x<0){
            return false;
        }else{
            while(x>0){
                digits.push_back(x%10);
                x = x/10;
            }

            while(y>0){
                if(y%10 == digits.back()){
                    y = y/10;
                    digits.pop_back();
                }else{
                    return false;
                }

            }
            return true;

        }
    }
};
```


this code worked, however it took 12 milliseconds to compile. I think time complexity here is O(2n) maybe it can be solved with log or even just n.


best solution here with fastest run:


``` C++

class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        if (x < 10) {
            return true;
        }
        auto b0 = 1, b1 = 1000000000;
        while (x / b1 == 0) {
            b1 /= 10;
        }
        for(; b0 < b1; b0 *= 10, b1 /= 10) {
            auto d0 = x / b0 % 10;
            auto d1 = x / b1 % 10;
            // cout << b0 << ' ' << b1 << endl;
            if (d0 != d1)  {
                return false;
            }
        }
        return true;
        // vector<int> digits;
        // digits.reserve(10);
        // while (x > 0) {
        //     digits.push_back(x % 10);
        //     x /= 10;
        // }
        // for (size_t x = 0, y = digits.size() - 1; x < y; ++x, --y) {
        //     if (digits[x] != digits[y]) {
        //         return false;
        //     }
        // }
        // return true;
    }
};

```

here they used the fact that for numbers less than 10 it is given that they are palindrome. The other interesting thing is that they used the higher and lower bounds given by assignment. According to ChatGPT and me actually seeing this afterwards, vector allocation of memory on larger arrays fails to give better perfomance, thus using even larger arrays is more efficient.




