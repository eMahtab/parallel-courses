# Parallel Courses
## https://leetcode.com/problems/parallel-courses

You are given an integer n, which indicates that there are n courses labeled from 1 to n. You are also given an array relations where relations[i] = [prevCoursei, nextCoursei], representing a prerequisite relationship between course prevCoursei and course nextCoursei: course prevCoursei has to be taken before course nextCoursei.

In one semester, you can take any number of courses as long as you have taken all the prerequisites in the previous semester for the courses you are taking.

Return the minimum number of semesters needed to take all courses. If there is no way to take all the courses, return -1.


# Implementation : Topological Sort
```java
class Solution {
    public int minimumSemesters(int n, int[][] relations) {
        int completed = 0;
        int semester = 0;
        int[] indegree = new int[n];
        for(int[] relation : relations) {
            indegree[relation[1] - 1]++;
        }
        
        Queue<Integer> q = new ArrayDeque<>();
        for(int i = 0; i < n; i++) {
            if(indegree[i] == 0) {
                q.add(i);
            }
        }
        
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i = 0; i < size; i++) {
                int course = q.remove();
                completed++;
                for(int[] relation : relations) {
                    if( (relation[0] - 1) == course) {
                        indegree[relation[1] - 1]--;
                        if(indegree[relation[1] - 1] == 0) {
                            q.add(relation[1] - 1);
                        }
                    }
                }
            }
            semester++;
        }
        return completed == n ? semester : -1;
    }
}
```
