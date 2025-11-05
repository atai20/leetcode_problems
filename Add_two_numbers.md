The problem: https://leetcode.com/problems/add-two-numbers/
<img width="461" height="423" alt="image" src="https://github.com/user-attachments/assets/0f50c311-53aa-478a-bcfd-cea8103d4493" />

my proposed solution with the plan:
```code C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */


 // My strategy here is to add them up one by one and add more members to each consecutive one if the number is bigger than 9. Maybe we can do that by adding 1 to next consequtive and have at the same place the mod of 10 of that number. 
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int additional = 0;
        ListNode * result = new ListNode;
        ListNode * head = result;
        while (l1->next != NULL || l2->next != NULL){
            result->val = (l1->val+l2->val)%10 + additional;
            additional = l1->val+l2->val/10;
            result = result->next;

        }

        return head;
    }
};
```
