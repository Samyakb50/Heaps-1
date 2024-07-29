# Heaps-1

## Problem1 
Kth largest in Array (https://leetcode.com/problems/kth-largest-element-in-an-array/)

class Solution {
public:
    void swap(int *a, int *b){
        int temp = *a;
        *a = *b;
        *b= temp;
    }
    int partition(vector<int>& nums, int start, int end) {
        int pi = end;
        int left = start;
        int i;
        for(i=start; i<end; i++){
            if(nums[i]<nums[pi]){
                swap(&nums[i], &nums[left]);
                left++;
            }
        }
        swap(&nums[left], &nums[pi]);
        return left;
    }
    int findKth(vector<int>& nums, int start, int end, int k){
        while(start<=end){
            // int mid = start + (end-start)/2;
            int pi = partition(nums, start, end);
            if(pi == (k)){
                return nums[k];
            }
            else if((k)<pi)
                return findKth(nums, start, pi-1, k);
            else
                return findKth(nums, pi+1, end, k);
        }
        return 0;
    }
    int findKthLargest(vector<int>& nums, int k) {
        int n = nums.size()-1;
        if(n==0){
            return nums[0];
        }
        return findKth(nums, 0, n, nums.size()-k);
    }
};

## Problem2

Merge k Sorted Lists(https://leetcode.com/problems/merge-k-sorted-lists/)

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode Merge2List(ListNode l1, ListNode l2){
        ListNode temp, mergeList;
        if(l1==null)
            return l2;
        if(l2==null)
            return l1;
        if(l1.val<l2.val)
        {
            mergeList=l1;
            l1=l1.next;
        }
        else{
            mergeList=l2;
            l2=l2.next;
        }
        temp = mergeList;
        while(l1!=null && l2!=null){
            if(l1.val<l2.val)
            {
                temp.next=l1;
                temp=temp.next;
                l1=l1.next;
            }
            else{
                temp.next=l2;
                temp=temp.next;
                l2=l2.next;
            }
        }
        if(l1!=null){
            temp.next=l1;
        }
        else{
            temp.next=l2;
        }
        return mergeList;
    }
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists ==null || lists.length ==0) return null;
        int n=lists.length-1;
        while(n!=0){
            int start = 0, end =n;
            while(start<end){
                lists[start] = Merge2List(lists[start++], lists[end--]);
                if(start>=end){
                    n = end;
                }
            }
        }
        return lists[0];
    }
}