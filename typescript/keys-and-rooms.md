
  # keys-and-rooms

  ```typescript
  function canVisitAllRooms(rooms: number[][]): boolean {
  const n = rooms.length;
  const visited = new Array(n).fill(false);
  visited[0] = true;
  const stack: number[] = [0];

  while (stack.length > 0) {
    const room = stack.pop()!;
    for (const key of rooms[room]) {
      if (!visited[key]) {
        visited[key] = true;
        stack.push(key);
      }
    }
  }

  return visited.every((room) => room);
}

  ```
  