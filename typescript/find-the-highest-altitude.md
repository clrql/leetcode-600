
  # find-the-highest-altitude

  ```typescript
  function largestAltitude(gain: number[]): number {
  let maxAltitude = 0; // Maximum altitude
  let currentAltitude = 0; // Current altitude

  for (let i = 0; i < gain.length; i++) {
    currentAltitude += gain[i]; // Update the current altitude
    maxAltitude = Math.max(maxAltitude, currentAltitude); // Update the maximum altitude
  }

  return maxAltitude;
}

  ```
  