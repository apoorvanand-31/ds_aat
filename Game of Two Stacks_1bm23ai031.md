#!/bin/python3

import math
import os
import random
import re
import sys

#
# Complete the 'twoStacks' function below.
#
# The function is expected to return an INTEGER.
# The function accepts following parameters:
#  1. INTEGER maxSum
#  2. INTEGER_ARRAY a
#  3. INTEGER_ARRAY b
#

def twoStacks(maxSum, a, b):
    # Write your code here
    # Initialize variables
    sum_elements = 0
    count = 0
    i = 0  # Pointer for stack a
    j = 0  # Pointer for stack b
    
    # Pop elements from stack a as long as the sum is within the limit
    while i < len(a) and sum_elements + a[i] <= maxSum:
        sum_elements += a[i]
        count += 1
        i += 1
    
    # Now try to pop elements from stack b, ensuring the sum stays within the limit
    while j < len(b) and sum_elements + b[j] <= maxSum:
        sum_elements += b[j]
        count += 1
        j += 1
    
    # Now try to pop elements from stack b while removing from stack a if necessary
    max_count = count
    while j < len(b):
        sum_elements += b[j]
        count += 1
        j += 1
        
        # If the sum exceeds the limit, remove elements from stack a
        while sum_elements > maxSum and i > 0:
            i -= 1
            sum_elements -= a[i]
            count -= 1
        
        # If the sum is valid, update the max_count
        if sum_elements <= maxSum:
            max_count = max(max_count, count)
    
    return max_count



if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    g = int(input().strip())

    for g_itr in range(g):
        first_multiple_input = input().rstrip().split()

        n = int(first_multiple_input[0])

        m = int(first_multiple_input[1])

        maxSum = int(first_multiple_input[2])

        a = list(map(int, input().rstrip().split()))

        b = list(map(int, input().rstrip().split()))

        result = twoStacks(maxSum, a, b)

        fptr.write(str(result) + '\n')

    fptr.close()
