Weighted Activity Selection
=====================

Description:
-------------
The weighted activity selection problem is a combinatorial optimization problem which calculates the highest weight one can get from performing non-conflicting activities within a given time frame. It also returns a list of respective activities.
The algorithm uses dynamic programming to break up the problem into a series of overlapping subproblems and build up solutions to larger and larger subproblem.

**Optimal substructure**

The algorithm calculates the maximum weight for activities 1 ... j where j is some activity from the set. If the algorithm selects activity j, it should add the activity's weight to the optimal solution to the problem which consists of remaining compatible activities calculated in one of the previous iterations.

**Overlapping subproblems**

Different activities can have the same set of compatible jobs which means that by memoizing the solutions to such subproblems we can dramatically decrease the time complexity.

**Complexity**

A brute-force recursive solution to this problem is correct but spectacularly slow
because of redundant sub-problems discussed above. As a result, it has exponential time complexity. The dynamic programming solution has a complexity O(n^2). This algorithm uses binary search to find the previous activity which decreases the complexity to O(nlogn).

In this implementation, the algorithm first sorts the activities by their finish time, which requires O(nlogn). For each j, it finds the previous compatible activity using binary search O(logn). As we have to repeat this procedure n times, it results in the complexity of O(nlogn). Constructing a list of selected activities also requires O(nlogn) in the worst case as the algorithm loops through the reversed list (n) and searches for the previous activity (logn). The resulting complexity is O(nlogn) + O(nlogn) + O(nlogn) --> O(nlogn).

Example implementation:
-----------------------------
Suppose you are a CEO in a small company and you need to attend a set of meetings to raise funds for a new project. Unfortunately, you can only attend one meeting at a time and some of them are overlapping. Each meeting has start and end times and a weight associated with it that corresponds to the amount of money you will raise if you attend it. The algorithm finds the highest profit you can get in such a situation and prints out the list of meetings you should attend.

Here's an example case:

|Names|a|b|c|d|
|----------|--------|----------|---------|----------|
|   **Weight**|   **$300**|   **$250**|   **$400**|   **$450**|
|**Start/End** |**9:00-13:00**|**11:00-14:00**|**16:00-18:00**|**15:00-21:00**|

In this example, activities a, b and and c, d overlap. That's why the algorithm will choose 2 activities which generate the highest profit - a and d - which will give you a total of $750.

**The input** of this algorithm is a list of activities with their names, start and finish times, and weights in any order:   
```python
meetings = [activity("b", 11, 14, 250), activity("a", 9, 13, 300), activity("c", 16, 18, 400), activity("d",15, 21, 450)]   
```
To **run** the algorithm, you should simply call the function "actselectw":  
```python
print actselectw(meetings)  
```
**The output** is the maximum weight possible for this set of activities and the activities which have been selected by the algorithm.
```python
Max weight is 750. You should pick activities ['a', 'd'].  
```
A link to the GitHub repository: https://github.com/ritakurban/actselectw          
