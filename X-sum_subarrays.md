Problem:https://leetcode.com/problems/find-x-sum-of-all-k-long-subarrays-i/?envType=daily-question&envId=2025-11-04
<img width="734" height="429" alt="image" src="https://github.com/user-attachments/assets/dc0b64cf-65ae-4720-b039-f9bea8833bdd" />


General idea
![unnamed](https://github.com/user-attachments/assets/35b4db37-8f71-4894-950e-1756047596b3)




proposed solution:
```C++
class Solution {
public:
    vector<int> findXSum(vector<int>& nums, int k, int x) {
        // plan is to do the traversion through the k elements, create an array of length k, if element 1 is equal to element 2, add them together, put it to the array, do so k times in the end get to array smaller than k, get top x of the elements from the array (maybe better use linked list with bigger elements to the right) after doing so output the vector.

        vector<int> values;
        vector<int> instances;
        
        
        for(int i = 0; i<k; i++){
            for(int i2 = i+1; i2<nums.size(); i2++){
                    if(values == NULL){
                        values.push_back(nums[i2]);
                        instances.push_back(1);
                    }else{
                        for(int i3 = 0; i3<values.size(); i3++){
                            if(values[i3]==nums[i2]){
                                instances[i3] += 1;
                            }else{
                                values.push_back(nums[i2]);
                                instances.push_back(1);
                            }
                        }                     
                    }
            }

            int biggest = 0;
            for(int i = 0; i<instances.size()){
                
                if(biggest<instances[i]){
                    biggest = instances[i];
                }
                
            }



            }
                


        }
        

    }
};
```
