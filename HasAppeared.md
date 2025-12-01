https://neetcode.io/problems/duplicate-integer/question
```C++
class Solution {
public:
    bool hasDuplicate(vector<int>& nums) {
        int sum = 0;
        for (int i = 0; i<nums.size(); i++){
            for (int i2 = 0; i2<nums.size(); i2++){
                if(i!=i2 && nums[i] == nums[i2]){
                    return true;
                }
            }
        }
        return false;
    }
};
```
