
  # course-schedule-ii

  ```javascript
  /**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {number[]}
 */
var findOrder = function(numCourses, prerequisites) {
  const adjacencyList = new Array(numCourses).fill(0).map(() => []);
  const indegree = new Array(numCourses).fill(0);
  const result = [];
  
  // Build the adjacency list and calculate the indegree of each course
  for (let [course, prerequisite] of prerequisites) {
    adjacencyList[prerequisite].push(course);
    indegree[course]++;
  }
  
  const queue = [];
  
  // Add all the courses with indegree 0 to the queue
  for (let i = 0; i < numCourses; i++) {
    if (indegree[i] === 0) {
      queue.push(i);
    }
  }
  
  // Perform topological sorting
  while (queue.length) {
    const prerequisite = queue.shift();
    result.push(prerequisite);
    
    for (let course of adjacencyList[prerequisite]) {
      indegree[course]--;
      
      if (indegree[course] === 0) {
        queue.push(course);
      }
    }
  }
  
  // If there is a cycle, it is impossible to finish all courses
  if (result.length !== numCourses) {
    return [];
  }
  
  return result;
};

  ```
  