# Maximum-Swap

You are given an integer num. You can swap two digits at most once to get the maximum valued number.

Return the maximum valued number you can get.

 

Example 1:

Input: num = 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
Example 2:

Input: num = 9973
Output: 9973
Explanation: No swap.
 

Constraints:

0 <= num <= 108

# SOLUTION

* Approach
Track the last occurrence of each digit: We store the last position of every digit (from 0 to 9) in an array, allowing us to know where the highest digits appear.
Identify a potential swap: As we traverse the number, for each digit, we check if there's a larger digit appearing later. If we find one, we swap the two digits.
Return the result: Once the optimal swap is performed (if any), return the new number. If no swap is needed, return the original number.
Complexity
Time complexity:
O(n), where (n) is the number of digits in the input number. We traverse the number twice: once to store the last occurrence of each digit, and once to find the optimal swap.

Space complexity:
O(1), since we only use an array of fixed size (10) to store the last occurrences of digits.

* JAVA CODE

class Solution {

    public int maximumSwap(int num) {
    
        // Convert number to string for digit manipulation
        
        char[] numArr = Integer.toString(num).toCharArray();
        
        int n = numArr.length;

        // Track the last occurrence of each digit (0-9)
        
        int[] last = new int[10];
        
        for (int i = 0; i < n; i++) {
        
            last[numArr[i] - '0'] = i;
        }

        // Traverse the number from left to right
        
        for (int i = 0; i < n; i++) {
        
            // Check if we can find a larger digit to swap
            
            for (int d = 9; d > numArr[i] - '0'; d--) {
            
                if (last[d] > i) {
                
                    // Swap and return the new number
                    
                    char temp = numArr[i];
                    
                    numArr[i] = numArr[last[d]];
                    
                    numArr[last[d]] = temp;
                    
                    return Integer.parseInt(new String(numArr));
                    
                }
            }
        }

        // Return the original number if no swap occurred
        
        return num;
    }
}

Step-by-Step Detailed Explanation

* Tracking last occurrence of digits:
We iterate through the number's digits and store the last occurrence of each digit (0-9). This helps us quickly look up where a larger digit might be located in the number.

* Traversing the number:
We traverse the digits of the number from left to right. For each digit, we check if there is any larger digit that appears after the current digit. If a larger digit exists, we can perform a swap to maximize the number.

* Performing a swap:
As soon as we find a larger digit that can be swapped with the current digit, we perform the swap. This is done because we are allowed only one swap to maximize the number. After the swap, we return the new number immediately.

* Returning the result:
If no swap was performed (because the number was already in its maximum form), we simply return the original number.
