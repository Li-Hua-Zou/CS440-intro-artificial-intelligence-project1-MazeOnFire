# intro-artificial-intelligence
This is a group project.

for all the maze except fire predict maze

1 for good cell
0 for obstacle p
2 for fire
0.5 for the potential way
0.3 for the way we walked （strategy1, 2, 3 only）

for fire predict maze

0 for fire
-1 for obstacle and the cell that fire can never reach
from 1 to infinity is the the fastest steps that fire can reach this grid

Steps For Usage
1. run the python
2. input dimension p (Separate by blank(" "))  (and q for strategy1, 2, 3)
3. you will see the preview for the maze (graph)
4. after you Turn off preview for the maze (graph), the code will run and give you a path(graph2)  (you will see fire graph  in strategy1, 2, 3.) if u can not see the graph2 code will print something to let you know what happened. e.g no way out
5. after u turn off the final graph2. done.

"no way out" or "just a bad maze. no way out"  means bad maze  no path out 
"you reach the goal" means you reach the goal
"u have been burned" means  you  have been burned and code will print where you were burned    e.g (3,6)
"Juat a bad maze or Fire or/and obstacles are blocking you. No way out" means  bad maze  no path out   OR  The fire blocked your way, you have no way to go   (only for  strategy2, 3. )


In order to predict the shortest number of steps from the fire to each grid, I first wrote a method predict_spread(maze). 
In this method, all the fire point coordinates will be stored in the list fires; each coordinate fire[k] in fires will be regarded as a fire point, 
and the prediction recursive method spread_once when there is only one fire point is called repeatedly.

There are six parameters for spread_once:
1. maze: the original maze; 0 represents the wall, 1 represents the road, and 2 represents the fire
2. accessed: the coordinates that have been accessed; return value
3. Predict: A two-dimensional list, the same size as the maze, to predict the spread of the fire, the initial value is -1. 
Among them, -1 represents the place where the fire did not burn, 0 to infinity represents the minimum number of steps the fire burns to this grid; another return value
4. fire: the coordinates of the fire and the coordinates currently being operated
5. prev: dictionary, key is the current coordinate, value is the coordinate of the previous operation
6. Queue: coordinates to be processed

First, judge whether to assign predict or return predict by judging whether the coordinate fire currently being processed can be found in accessed and prev. If fire is not in prev, then predict[fire[0]][fire[1]] == 0, 
which means this is the initial fire point. If there is fire in prev, then it depends on whether fire is accessed. Generally, the number stored in this grid of predict is the number of the last visited grid plus one. 
However, if the current grid has been accessed and the number of the current grid is smaller than the number of the previous grid plus one, 
it means that the new fire does not cover the old fire, so do not change the current grid and return directly. 
Then use predict the current coordinates of fire to determine whether the four grids of fire up, down, left and right meet the conditions that can be spread 
(the grids around the current coordinates of the original maze are 1 and whether they touch the boundary, etc.), and add the eligible coordinates to the queue and prev .
 At the end, store the first coordinate of the queue as the new fire coordinate and call spread_once. When the recursion is complete, return predict and accessed.
