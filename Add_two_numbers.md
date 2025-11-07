The problem: 
https://leetcode.com/problems/add-two-numbers/ </br>
<img width="461" height="423" alt="image" src="https://github.com/user-attachments/assets/0f50c311-53aa-478a-bcfd-cea8103d4493" />

my proposed solution with the plan:
```C++
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

Revised version still not working:
```C++
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
     //   int additional = 0;
     //   ListNode * result = new ListNode(5);
     //   ListNode * head = result;
     //   while (l1->next != NULL || l2->next != NULL){
     //       result->val = (l1->val+l2->val)%10 + additional;
     //       additional = l1->val+l2->val/10;
     //       result->next = new ListNode(5);
      //      result = result->next;
      //      l1 = l1->next;
        //    l2 = l2->next;

       // }
        int additional = 0;
        ListNode * result = new ListNode(0);
        ListNode * head = result;
        while (l1->next != nullptr || l2->next !=nullptr){
            result->val = (l1->val+l2->val + additional)%10;
            additional = (l1->val+l2->val+additional)/10;
            result->next = new ListNode(0);






            //very important new part I just learnt \/
            if (result) result = result->next;
            if (l1) l1 = l1->next;
            if (l2) l2 = l2->next;
        }
        result->val = (l1->val+l2->val + additional)%10;

        return head;
    }
};
```

Fixed better version:

```C++

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

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummyHead = new ListNode(0);  // starting node
        ListNode* current = dummyHead;
        int carry = 0;

        while (l1 != nullptr || l2 != nullptr || carry != 0) {
            int val1 = (l1 != nullptr) ? l1->val : 0;
            int val2 = (l2 != nullptr) ? l2->val : 0;

            int sum = val1 + val2 + carry;
            carry = sum / 10;
            int digit = sum % 10;

            current->next = new ListNode(digit);
            current = current->next;

            if (l1 != nullptr) l1 = l1->next;
            if (l2 != nullptr) l2 = l2->next;
        }

        return dummyHead->next;  // skip the dummy node
    }
};


```
