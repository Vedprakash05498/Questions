# Questions

'''
Given an array A of integers, we must modify the array in the following way:

we choose an i and replace A[i] with -A[i], and we repeat this process K times in total. 

(We may choose the same index i multiple times.)

Return the largest possible sum of the array after modifying it in this way.
 
Example 1:

Input: A = [4,2,3], K = 1

Output: 5

Explanation: Choose indices (1,) and A becomes [4,-2,3].

Example 2:

Input: A = [3,-1,0,2], K = 3

Output: 6

Explanation: Choose indices (1, 2, 2) and A becomes [3,1,0,2].

Example 3:

Input: A = [2,-3,-1,5,-4], K = 2

Output: 13

Explanation: Choose indices (1, 4) and A becomes [2,3,-1,5,4].
 
Note:

1 <= A.length <= 10000

1 <= K <= 10000

-100 <= A[i] <= 100
'''

class Solution(object):

    def largestSumAfterKNegations(self, A, K):
        """
        :type A: List[int]
        :type K: int
        :rtype: int
        """
        A.sort()
        index = 0
        while K > 0:
            if A[index] < 0:
                A[index] *= -1
                if A[index+1] < A[index] and index < len(A)-1:
                    index += 1
            else:
                A[index] *= -1
            K -= 1
        return sum(A)
        
        
        
        This code defines a class Solution and a method largestSumAfterKNegations within that class. The method takes two arguments, a list of integers A and an integer K, and returns an integer representing the maximum sum that can be obtained by changing at most K values in A to their negatives.

The implementation first sorts the input list A in non-decreasing order using the sort() method. It then initializes an index variable index to 0, which will be used to traverse the list.

The while loop continues as long as there are still values to be negated (K > 0). Within the loop, the code checks if the current element of A at index index is negative (A[index] < 0). If it is, then the code negates the element by multiplying it by -1 (A[index] *= -1).

If the next element in the list is smaller than the current one (in absolute value), and the current element is not the last element in the list (index < len(A)-1), then the code increments the index variable index by 1, so that the next iteration of the loop negates the next smallest value.

If the current element is not negative, the code simply negates it as well.

Finally, the function returns the sum of the updated list A using the built-in sum() function.

In summary, the function sorts the input list A, negates the smallest K values in the list, and returns the sum of the updated list.
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        This code implements a function that takes a list of integers A and an integer K, and returns the maximum sum that can be obtained by changing at most K values in A to their negatives.

The approach taken by the code is to first sort the list A, and then iterate over it K times, changing the sign of the smallest negative number in the list, or the smallest positive number if there are no negative numbers left. If the sign of a number is changed, the index variable is incremented to point to the next number in the list.

The function then returns the sum of the updated list.

The implementation seems correct, but there are a few things that could be improved. First, the code assumes that the list A is not empty, which could lead to an IndexError if A is empty. A check for this case should be added at the beginning of the function.

Second, the code could be made more efficient by avoiding the need to sort the list A. Since the function only needs to find the smallest K numbers in the list, a heap-based algorithm could be used to maintain a priority queue of the smallest K numbers in A, and the sign of each of these numbers could be changed in turn. This would have a time complexity of O(N log K), where N is the length of the list A.

Third, the code could be made more readable by using more descriptive variable names. For example, the variable A could be renamed to nums, and the variable index could be renamed to i.


import heapq

class Solution(object):

    def largestSumAfterKNegations(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if not nums:
            return 0

        heap = []
        for num in nums:
            heapq.heappush(heap, num)

        for i in range(k):
            if heap[0] >= 0:
                break
            num = heapq.heappop(heap)
            heapq.heappush(heap, -num)

        return sum(heap)
        
        
        
        
        
        
        
        
        
        
        # Question2
        ''
In a list of songs, the i-th song has a duration of time[i] seconds. 
Return the number of pairs of songs for which their total duration in seconds is divisible by 60.  Formally, we want the number of indices i < j with (time[i] + time[j]) % 60 == 0.
 
Example 1:
Input: [30,20,150,100,40]
Output: 3
Explanation: Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
Example 2:
Input: [60,60,60]
Output: 3
Explanation: All three pairs have a total duration of 120, which is divisible by 60.
Note:
1 <= time.length <= 60000
1 <= time[i] <= 500
'''

class Solution(object):
    def numPairsDivisibleBy60(self, time):
        """
        :type time: List[int]
        :rtype: int
        """
        count_arr = [0]*60
        result = 0
        for t in time:
            remainder = t%60
            complement = (60-remainder)%60
            result += count_arr[complement]
            count_arr[remainder] += 1
        return result
 
 '''
	Explanation: 
	Q1: why create array of size 60? 
		it is similar to the map which store the count. Why only 60 because 60 modulo of number cannot be more than 60
	Q2: why we need complement?
		to check the pair if it exisit with given value or not example: if remainder is 20 then we need to check if we have any number with remainder 40 or not.
	Q3: why 60 modulo complement?
		for handle cause when remainder is zero 
 '''



# question3

Given a m * n matrix of ones and zeros, return how many square submatrices have all ones.

 

Example 1:

Input: matrix =
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15

Explanation: 

There are 10 squares of side 1.

There are 4 squares of side 2.

There is  1 square of side 3.

Total number of squares = 10 + 4 + 1 = 15.

Example 2:

Input: matrix = 
[
  [1,0,1],
  [1,1,0],
  [1,1,0]
]
Output: 7
Explanation: 

There are 6 squares of side 1.

There is 1 square of side 2. 

Total number of squares = 6 + 1 = 7.
 

Constraints:

1 <= arr.length <= 300

1 <= arr[0].length <= 300

0 <= arr[i][j] <= 1


# sollution 
class Solution:

    def countSquares(self, matrix: List[List[int]]) -> int:
    
        m, n = len(matrix), len(matrix[0])
        
        dp = [[0] * n for _ in range(m)]
        
        count = 0
        
        for i in range(m):
        
            for j in range(n):
            
                if matrix[i][j] == 1:
                
                    if i == 0 or j == 0:
                    
                        dp[i][j] = 1
                        
                    else:
                    
                        dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
                        
                    count += dp[i][j]
        
        return count
        
        
        
        programming to keep track of the largest square that can be formed at each position in the input matrix. Specifically, the dp[i][j] value
        
        represents the size of the largest square with matrix[i][j] as its bottom-right corner.

To compute dp[i][j], we observe that the largest square with matrix[i][j] as its bottom-right corner must be made up of squares with matrix[i-1][j],

matrix[i][j-1], and matrix[i-1][j-1] as their bottom-right corners. We take the minimum of the dp values corresponding to these positions,

add 1 to it (to account for the new square with matrix[i][j] as its bottom-right corner), and assign the result to dp[i][j].

Finally, we sum up all the values in the dp matrix to obtain the total count of square submatrices with all ones in the input matrix.









# Question 4

# Python code to find the average of a list of numbers:

def find_average(numbers):

    # Check if the list is empty
    
    if not numbers:
    
        return 0
    
    # Calculate the sum of the numbers
    
    total = sum(numbers)
    
    # Calculate the average
    
    average = total / len(numbers)
    
    return average

To use this function, simply pass in a list of numbers as an argument, like this:

numbers = [2, 4, 6, 8, 10]

average = find_average(numbers)

print("The average is:", average)

This will output:

The average is: 6.0

You can replace the list of numbers with your own list to find the average of any set of numbers.


# Question 5

"counting apple problems" and the problem is as follows:

There are n people with two types of food, apples and oranges. Each person can either have an apple or an orange or none at all. How many different ways

are there for the distribution of apples and oranges among the n people?

To solve this problem, we can use the concept of permutations and combinations.

Let's say there are k people who have been given apples. Then, the number of people who have been given oranges would be n - k. We can distribute apples

among n people in nCk ways (n choose k). And since each of these ways corresponds to a unique distribution of oranges as well, we need to multiply nCk by

(n-k)C(n-k) to get the total number of distributions.

Therefore, the total number of distributions of apples and oranges among n people is:

Σ (nCk * (n-k)C(n-k)), k=0 to n

where Σ denotes summation. This expression can be simplified using the identity nCk = nC(n-k), to get:

Σ (nCk)², k=0 to n/2

where n/2 denotes the integer division of n by 2.

So the final answer to the problem is the summation of nCk squared for k ranging from 0 to n/2.



import math

def count_distributions(n):

    count = 0
    
    for k in range(n//2 + 1):
    
        count += math.comb(n, k)**2
	
    return count

# Example usage
n = 5

distributions = count_distributions(n)

print(f"There are {distributions} ways to distribute apples and oranges among {n} people.")




In this code, we use the math.comb() function to calculate the binomial coefficient (i.e., n choose k) and then sum up the squares of these coefficients

for k ranging from 0 to n/2. The // operator performs integer division in Python 3, which is used to ensure that we only iterate over k values up to n/2.

Note that this code assumes that n is a non-negative integer. If n can be negative or a non-integer, you may need to add some additional error checking to

the code.


