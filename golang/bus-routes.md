
  # bus-routes

  ```golang
  func numBusesToDestination(routes [][]int, source int, target int) int {
	if source == target {
		return 0
	}

	stopToRoutes := make(map[int][]int)
	for i, route := range routes {
		for _, stop := range route {
			stopToRoutes[stop] = append(stopToRoutes[stop], i)
		}
	}

	visitedRoutes := make([]bool, len(routes))
	visitedStops := make(map[int]bool)

	queue := list.New()
	queue.PushBack(source)
	steps := 0

	for queue.Len() > 0 {
		size := queue.Len()

		for i := 0; i < size; i++ {
			currentStop := queue.Remove(queue.Front()).(int)

			for _, routeIndex := range stopToRoutes[currentStop] {
				if visitedRoutes[routeIndex] {
					continue
				}

				visitedRoutes[routeIndex] = true

				for _, nextStop := range routes[routeIndex] {
					if nextStop == target {
						return steps + 1
					}

					if !visitedStops[nextStop] {
						visitedStops[nextStop] = true
						queue.PushBack(nextStop)
					}
				}
			}
		}

		steps++
	}

	return -1
}
  ```
  