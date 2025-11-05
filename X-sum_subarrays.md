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

The code does not even compile, I am stuck with the last step where according to my idea you should sort it out in the end and get top x out from them. I think better solution would have been dynamically sort the instance array, however we would have to also do it for the values array. I think the best solution here would have been with hash tables implementation of which I don't know yet. But we will see on the actual solution.


Solution from Leetcode themselves:

Approach: Hash Table + Sorting
Intuition

We enumerate all subarrays of length k, using a hash table cnt to count the occurrences of each number within the subarray. For each key-value pair (key,value) in the hash table—where key represents a number and value represents its occurrence count—we store them in an array and sort this array primarily in descending order by value, and secondarily in descending order by key.

After sorting, the first x tuples correspond to the x most frequent elements and their counts. By summing their products, we obtain the answer for this subarray.
Implementation

```C++

class Solution {
public:
    vector<int> findXSum(vector<int>& nums, int k, int x) {
        int n = nums.size();
        vector<int> ans;
        for (int i = 0; i <= n - k; ++i) {
            unordered_map<int, int> cnt;
            for (int j = i; j < i + k; ++j) {
                ++cnt[nums[j]];
            }

            vector<pair<int, int>> freq;
            for (const auto& [key, value] : cnt) {
                freq.emplace_back(value, key);
            }
            sort(freq.begin(), freq.end(), greater<pair<int, int>>());

            int xsum = 0;
            for (int j = 0; j < x && j < freq.size(); ++j) {
                xsum += freq[j].first * freq[j].second;
            }
            ans.push_back(xsum);
        }
        return ans;
    }
};

```
Complexity Analysis

    Time complexity: O(n×klogk).

    The time to enumerate all subarrays of length k is O(n), and each subarray takes O(klogk) time for sorting and computing the answer.

    Space complexity: O(k).

    This is the space required for hash table and arrays.

As we can see here it was exactly as I thought with hash function implementation and sorting algorithms, all that is left for me is to take into account this method for future reference.



