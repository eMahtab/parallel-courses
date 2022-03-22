# Parallel Courses
## https://leetcode.com/problems/parallel-courses


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
