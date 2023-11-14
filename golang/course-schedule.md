
  # course-schedule

  ```golang
  func canFinish(numCourses int, prerequisites [][]int) bool {
    // Create an adjacency list to represent the graph
    graph := make([][]int, numCourses)
    for _, prerequisite := range prerequisites {
        course, prerequisite := prerequisite[0], prerequisite[1]
        graph[course] = append(graph[course], prerequisite)
    }

    // Create an array to track the visited status of each course
    visited := make([]int, numCourses)

    // Perform depth-first search (DFS) on each course
    for course := 0; course < numCourses; course++ {
        if visited[course] == 0 && !dfs(course, graph, visited) {
            return false
        }
    }

    return true
}

func dfs(course int, graph [][]int, visited []int) bool {
    // If the course has already been visited and marked as being visited again, a cycle exists
    if visited[course] == -1 {
        return false
    }

    // If the course has already been visited and marked as visited, no cycle exists
    if visited[course] == 1 {
        return true
    }

    // Mark the course as being visited
    visited[course] = -1

    // Recursively visit the prerequisites of the course
    for _, prerequisite := range graph[course] {
        if !dfs(prerequisite, graph, visited) {
            return false
        }
    }

    // Mark the course as visited
    visited[course] = 1

    return true
}
  ```
  