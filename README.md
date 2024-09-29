# Minimum-Cost-for-Cutting-Cake-II

There is an m x n cake that needs to be cut into 1 x 1 pieces.

You are given integers m, n, and two arrays:

horizontalCut of size m - 1, where horizontalCut[i] represents the cost to cut along the horizontal line i.
verticalCut of size n - 1, where verticalCut[j] represents the cost to cut along the vertical line j.
In one operation, you can choose any piece of cake that is not yet a 1 x 1 square and perform one of the following cuts:

1. Cut along a horizontal line i at a cost of horizontalCut[i].
2. Cut along a vertical line j at a cost of verticalCut[j].
After the cut, the piece of cake is divided into two distinct pieces.
The cost of a cut depends only on the initial cost of the line and does not change.
Return the minimum total cost to cut the entire cake into 1 x 1 pieces.

import heapq

class Solution:

    def minimumCost(self, m, n, horizontalCut, verticalCut):
        cuts = [(-cost, 'H') for cost in horizontalCut] + [(-cost, 'V') for cost in verticalCut]
        heapq.heapify(cuts)
        
        horizontal_pieces = 1
        vertical_pieces = 1
        
        total_cost = 0
        
        while cuts:
            cost, cut_type = heapq.heappop(cuts)
            cost = -cost  
            
            if cut_type == 'H':
                total_cost += cost * vertical_pieces
                horizontal_pieces += 1
            else:
                total_cost += cost * horizontal_pieces
                vertical_pieces += 1
                
        return total_cost
