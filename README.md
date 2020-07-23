# 🌴Island Problem: What is Optimal 🌴

*[LeetCode Problem Link](https://leetcode.com/problems/island-perimeter/)*<br><br>
Today, we are going to apply a recursive DFS to solve LeetCode's Island perimeter problem in [O(mn) worst case time complexity](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-videos/lecture-10-understanding-program-efficiency-part-1/). This question is a part of the July Challenge. A great extension is solving the problem iterativly. Feel free to jump ahead or act as a resource for your peers if this is too easy. I can always use the help teaching!

- Understanding the time complexity of a DFS : [stackoverflow](https://stackoverflow.com/questions/34816910/complexity-of-a-recursive-dfs) 

- Time complexity : O(M×N) where M is the number of rows and N is the number of columns.

- Space complexity : O(min(M,N)) because in worst case where the grid is filled with lands, the size of queue can grow up to min(M,N)

**I make errors**<br>
Please call them out as you see them! Typically, my spelling, vairable names, and "approximations" when doing math.


**Music**<br>
I love music.
[Here's what I've](https://www.youtube.com/watch?v=-UaZDpF3bS0) been programming to lately. Please share your go-to's! If you want to work on an open-source js sound project, checkout [p5-sound](https://github.com/processing/p5.js-sound)

<img src='https://i.pinimg.com/736x/86/53/20/865320144640b89e1c6baed9d49785f4.jpg' height="200">

**After Solving**<br>
Is this the best solution? What is optimal || what could be changed to make this more optimal?

---
---

**Key Steps**

| Timing | Type | Topic |
| --- | --- | --- |
| 05 min | [Setting up the Helper Method](#opening) |OOP Setup  |
| 10 min | [Where to Start](#codealong1)  | Bounds of the problem|
| 10 min | [Recurrence](#dfs)  | What drives this DFS?|
| 05 min | [Debugging](#debugging) |Tracing a program |
| Extra  | [🥱I'm way ahead](#extension) | Google's Most Asked Question |


<a name="opening"></a>
##  🌱Setting up the Helper Method 🌱

```txt
 loop through the matrix:
    if land:
        answer = self.helperFunction(para1, para2, para2...)
        return answer
return False
```

The idea here is we want to cycle through the matrix until we find a piece of the island and then run a dfs. I love setting up problems like this by using a helper function to solve/ acutallay do the computation. For example,


![img](https://img.c4learn.com/2012/04/Multi-Dimensional-Array-in-C-Programming.gif)


Take a few minuets to find out how you iterate over a matrix in Python. The answers are below. The idea isn't to bore you with a google search, but to get used to searching stackoverflow. I visit stackof about 3-5 times per day when working. We can't go in-depth here, but resources are linked.

- [Source](https://stackoverflow.com/questions/16548668/iterating-over-a-2-dimensional-python-list)

- [Further Reading](https://cs.nyu.edu/courses/fall16/CSCI-UA.0101-004/resources/lecture12.pdf)

- More info on [Python Classes](https://www.w3schools.com/python/python_classes.asp)


> What parameters should the helper function take in if using OOP?


**Iterate through matrix and call helper function**

  <details>
    <summary>Click to see code</summary>

```python
def islandPerimeter(self, grid: List[List[int]]) -> int:
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == 1:
                # calling our helper function
                # saving result of function in var p
                p = self.dfs(grid, i, j)
                    return p
    return 0 # if we go through the matrix without finding an island
```
  </details>


---
---

<a name="codealong1"></a>

## Where to Start -> Bounds of the Problem:
What is this problem actually asking? Meaning,

**Discussion**
- what do we want to count?
- how do we know what can be counted?
- how do we know when to end the program?

**Code-a-long OR code your own**<br>
> How does everyone feel about coding their own and then sharing answers?

**Create helper Function and Set Bounds**

  <details>
    <summary>Click to see code</summary>

```python
def dfs(self, grid, i, j):
        # out of bounds add 1
        if i < 0 or i > len(grid)-1 or j < 0 or j > len(grid[0])-1:
            return 1
        # if 0 add 1
        # we are counting 0's not 1's b/c that's the perimeter
        elif grid[i][j] == 0:
            return 1
        # if visited terminate search branch
        elif grid[i][j] == -1:
            return 0
        else:
            # recursive call(s) here
```
  </details>

---
---
<a name="dfs"></a>

## Recurrance: DFS 
[recursion review via tracing](https://www.youtube.com/watch?v=B3U6LExgevE)<br>
When programming our [DFS](https://medium.com/basecs/deep-dive-through-a-graph-dfs-traversal-8177df5d0f13), we want to make sure that we

- continue searching until the whole island is searched
- don't revisit a node
- have a way of keeping track of island's perimeter


**Iterate through matrix and call helper function**

  <details>
    <summary>Click to see code</summary>

```python
def dfs(self, grid, i, j):
        # out of bounds add 1
        if i < 0 or i > len(grid)-1 or j < 0 or j > len(grid[0])-1:
            return 1
        # if 0 add 1
        # we are counting 0's not 1's b/c that's the perimeter
        elif grid[i][j] == 0:
            return 1
        # if visited terminate search branch
        elif grid[i][j] == -1:
            return 0
        else:
            # recursive call(s) here
             # mark location as visited
            grid[i][j] = -1
            down = self.dfs(grid, i+1,j)
            up = self.dfs(grid, i-1, j)
            right = self.dfs(grid, i, j+1)
            left = self.dfs(grid, i, j-1)
            return down + up + right + left
```
  </details>


---
<a name="debugging"></a>

## Debugging, Tracing, & Optimizing:

- Take some time to optimize this program. How can one save space or time?
- How would you go about debugging this program?
- Anyone need a Team Debug session.

---
---
<a name="extension"></a>

## Extensions 
| Level  | Link                                                                    | Info                                     |
|--------|-------------------------------------------------------------------------|------------------------------------------|
| Easy   | [Post-order tree](https://leetcode.com/problems/n-ary-tree-postorder-traversal/)| Recursion Practice               |
| Medium | [Max Area of Island](https://leetcode.com/problems/max-area-of-island/) | Out of many Isle, find the largest       |
| Medium | [Word Search](https://leetcode.com/problems/word-search/)               | Find a word in a matrix                  |
| Medium | [Rotten Oranges](https://leetcode.com/problems/rotting-oranges/)        | Google's most asked question this summer |
| Medium | [Combo Sum](https://leetcode.com/problems/combination-sum/)             | Generate combos using bfs                |


*[Check out this youtube series](https://www.youtube.com/watch?v=TzoDDOj60zE) for a walkthrough of Rotten Oranges* and many other leetcode problems.

---
---

<details>
    <summary>Answer in JS 236 ms runtime</summary>

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
    for(i = 0; i < grid.length; i++){
        for(j = 0; j < grid[i].length; j++){
            if (grid[i][j] == 1){
                p = dfs(grid, i, j);
                return p;
            }
        }
    }
    return 0;
};

var dfs = function (grid, i, j){
    if (0 > i || i >= grid.length || 0 > j || j >= grid[0].length){
        return 1;
    }
    if (grid[i][j]==0){
        return 1;
    }
    
    if (grid[i][j] == 1){
        grid[i][j] = -1;
        return dfs(grid, i+1, j) + dfs(grid, i-1, j) + dfs(grid, i, j+1) + dfs(grid, i, j-1);
    }
    return 0;
}
```
  </details>

<details>
    <summary>Answer in Python 660ms runtime</summary>

```python3
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        for x in range(len(grid)):
            for y in range(len(grid[0])):
                if grid[x][y] == 1:
                    p = self.dfs(grid, x, y, 0)
                    return p
        return 0
    
    
    def dfs(self, grid, x, y, p):
        # out of bounds add 1
        if x < 0 or x > len(grid)-1 or y < 0 or y > len(grid[0])-1:
            return 1
        # if o add 1
        elif grid[x][y] == 0:
            return 1
        elif grid[x][y] == -1:
            return 0
        else:
            grid[x][y] = -1
            return  self.dfs(grid, x+1, y, 1) + self.dfs(grid, x-1, y, 1) + self.dfs(grid, x, y+1, 1) + self.dfs(grid, x, y-1, 1)
```
  </details>
  
<details>
    <summary>Answer in Java 11ms runtime </summary>

```java
class Solution {
    public int islandPerimeter(int[][] grid) {
        int count = 0;
        for(int i=0; i < grid.length; i++){
            for(int j=0; j < grid[i].length; j++){
                if(grid[i][j] == 1){
                    count = dfs(grid, i, j);
                    return count;
                }
            }
        }
        return count;
    }
    
    public int dfs(int[][] grid, int i, int j){
        // out of bounds return 1
        if (0 > i || i >= grid.length || 0 > j || j >= grid[0].length){
            return 1;
        }
        if (grid[i][j] == 0){
            return 1;
        }
        if (grid[i][j] == 1){
            grid[i][j] = -1;
            int d = dfs(grid, i+1, j);
            int u = dfs(grid, i-1, j);
            int l = dfs(grid, i, j-1);
            int r = dfs(grid, i, j+1);
            return d+u+l+r;
        }
        return 0;
    }
}
```
  </details>
